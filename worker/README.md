# Assistente Groq — AMV Conectar (GitHub Pages + Cloudflare Worker)

**Não é necessário mudar a hospedagem do site.** O GitHub Pages continua servindo os arquivos estáticos. Um Cloudflare Worker separado encaminha as mensagens para a Groq e mantém `GROQ_API_KEY` privada.

## O que já está preparado

- `assets/assistant-ai.js`: campo de conversa, histórico curto, perguntas rápidas e fallback.
- `assets/assistant-ai.css`: estilos complementares.
- `assets/assistant-config.js`: URL pública do backend (inicialmente vazia).
- `worker/src/index.js`: API `POST /chat` para a Groq.
- `worker/wrangler.jsonc`: configuração de origem permitida e limite aproximado de 10 solicitações/minuto por IP.

Enquanto `window.AMV_AI_ENDPOINT` estiver vazio, o FAQ antigo continuará funcionando normalmente. Nenhuma chave é necessária no repositório.

## Configuração na Cloudflare (somente backend)

1. Crie uma conta em https://dash.cloudflare.com/ e acesse **Workers & Pages → Workers** (não Pages).
2. Pelo computador, instale Node.js, abra um terminal na pasta `worker` e execute `npx wrangler login` e `npx wrangler deploy`. O arquivo `wrangler.jsonc` configura o rate limiting.
3. No painel do Worker: **Settings → Variables and Secrets → Add → Secret**. Nome: `GROQ_API_KEY`, valor: **uma chave nova** criada em https://console.groq.com/keys . Nunca digite essa chave no GitHub, no chat ou em `wrangler.jsonc`.
4. Confira **Settings → Variables**: `ALLOWED_ORIGIN=https://vizzahck.github.io` e `GROQ_MODEL=openai/gpt-oss-20b`. Se trocar o domínio do site no futuro, atualize `ALLOWED_ORIGIN`.
5. A URL do Worker será semelhante a `https://amv-groq-chat.SEUSUBDOMINIO.workers.dev`. Teste `https://...workers.dev/health` para verificar publicação.
6. Abra `assets/assistant-config.js` e configure `window.AMV_AI_ENDPOINT = "https://amv-groq-chat.SEUSUBDOMINIO.workers.dev/chat";`. **Esse endereço é público; a chave privada fica somente no Worker.**
7. Publique o site no GitHub Pages como antes. Faça perguntas à IA e confira se há erros no console do navegador.

## Testes antes de publicar

- Abra `index.html` antes de configurar o endpoint: o FAQ deve funcionar normalmente.
- Com o Worker implantado e a chave configurada, teste pergunta livre, sugestões rápidas, fechamento do chat e Nova conversa.
- Confirme que Formspree, WhatsApp, menu, temas, páginas e navegação continuam funcionando.
- Nunca inclua `GROQ_API_KEY` em arquivos do repositório, nem no JavaScript do navegador.

## Segurança e custos

- O código do Worker **não contém a chave**; lê apenas um Secret cadastrado no painel.
- Restrição de `Origin` e CORS não substituem autenticação. Um cliente não navegador pode falsificar Origin.
- O limite `AMV_RATE_LIMIT` é aproximado, por ponto de presença da Cloudflare; não é limite global rígido. IPs compartilhados podem ser afetados.
- Monitore cotas da Groq e da Cloudflare. Se precisar de garantia maior contra abuso, adicione Cloudflare Turnstile, limites estritos ou autenticação antes de disponibilizar amplamente.
- O Worker responde com erro amigável caso a Groq esteja indisponível ou sem cota. O site e o formulário continuam independentes.
- Revogue a antiga chave Groq compartilhada em conversas e gere uma nova.

**Atenção:** ao cadastrar o Worker por colagem manual no painel, o limitador declarado em `wrangler.jsonc` não é criado automaticamente. Para ativar a proteção de limite, faça o deploy com Wrangler ou configure uma proteção equivalente no painel.