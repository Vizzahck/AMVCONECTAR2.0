# AMV Conectar — versão estática completa

## Abrir no computador
Extraia toda a pasta e abra `index.html` no navegador. Não mova os arquivos HTML para fora da pasta: eles usam os recursos em `assets/`.

## Hospedar
Envie todo o conteúdo de `versao-estatica/` para a pasta pública de sua hospedagem. Não é necessário instalar programas, pacotes, React ou um serviço de servidor. Os endereços das páginas terminam em `.html`.

## Conteúdo
- `index.html`: página inicial com serviços, diferenciais, processo e contato.
- `quem-somos.html`, `missao.html`, `visao.html`, `valores.html`, `projeto-integrador.html`: páginas institucionais.
- `assets/site.css`: estilos e temas.
- `assets/theme.js`: tema inicial e preferência salva.
- `assets/site.js`: menu, troca de tema, assistente, validação e envio do formulário via Formspree.
- `assets/faq.js`: perguntas e respostas do assistente, sem IA ou serviço pago.
- `assets/*.png`: logos transparentes e favicon.
- `assets/manrope-*`: fontes locais.
- `assets/OFL-Manrope.txt`: licença da fonte Manrope.

## Funcionalidades e limites
O menu, o assistente, as seis páginas, imagens, ícones e fontes funcionam sem acesso à internet. Os links WhatsApp exigem internet e abrem https://wa.me/5598984833670.

O formulário de contato da página inicial está configurado para enviar os dados (nome, e-mail, empresa, assunto e mensagem) ao **Formspree** no endpoint `https://formspree.io/f/mgaawnyg`. Ele só exibe confirmação após resposta positiva do serviço. Se ocorrer erro, informa o problema e mantém os campos preenchidos. O Formspree exige conexão com a internet, conta ativa e e-mail de destino confirmado. Os envios e notificações ficam sujeitos às configurações e limites do serviço. A confirmação de entrega à caixa de e-mail deve ser verificada no painel do Formspree.

Para testar: publique no GitHub Pages, acesse a página de contato e envie uma mensagem de teste; confira o painel do Formspree e a caixa de entrada/spam do e-mail configurado. Abrir o arquivo `index.html` diretamente por `file://` pode bloquear o envio AJAX em certos navegadores devido a restrições de origem; nesse caso, teste pela hospedagem HTTP(S). Se o JavaScript estiver desabilitado, o formulário usa o envio HTML normal. Não insira chaves privadas nos arquivos estáticos.

A preferência claro/escuro é salva quando o navegador permite armazenamento local. Abrir arquivos diretamente pode restringir essa persistência em alguns navegadores; em uma hospedagem normal, ela é compartilhada entre as páginas.

O site existente não foi substituído: esta pasta é uma entrega independente em HTML, CSS e JavaScript puro. A logo superior é distinta da logo central e do rodapé, preservando as versões atuais sem fundo. Ícones SVG estão embutidos nos arquivos HTML.
