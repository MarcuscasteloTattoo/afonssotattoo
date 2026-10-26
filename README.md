# Afonso Tattoo

Landing page do tatuador Afonso: estilos e diferenciais, portfólio, "Quem sou" e formulário de orçamento que leva ao WhatsApp.

É um site estático: um `index.html` e a pasta `assets/` com as fotos. Não precisa de build nem de instalação. As fontes vêm do Google Fonts.

## Testar no computador

Abra o `index.html` no navegador (dois cliques no arquivo).

## Publicar

Funciona em qualquer hospedagem de site estático. Envie o `index.html`, o `favicon.png` e a pasta `assets/` juntos, mantendo a estrutura.

- **GitHub Pages:** suba os arquivos num repositório e ative em Settings → Pages → *Deploy from a branch* → `main` / `(root)`.
- **Netlify:** arraste a pasta inteira em app.netlify.com/drop.
- **Hostinger, Locaweb e similares:** envie os arquivos para a pasta `public_html`.

## Onde editar

No fim do `index.html`, dentro do `<script>`, o objeto `site` guarda o conteúdo que muda com frequência:

- `estilos`: os 4 cards do carrossel "Estilos e diferenciais" (título, texto e foto; usam fotos do portfólio).
- `portfolio`: as fotos de "Trabalhos recentes", na ordem em que aparecem. Para trocar ou acrescentar, coloque a foto em `assets/` e adicione `{ src: "assets/nome.webp", alt: "descrição" }`.
- `avaliacoes`: avaliações do Google (nome, tempo, texto), da mais recente para a mais antiga. A seção de avaliações foi retirada da página por enquanto; o código continua pronto para quando ela voltar.
- `whatsappNumero`: número com DDI e DDD, só dígitos (ex.: `5511999999999`). Com ele, o WhatsApp abre com o orçamento já escrito. Vazio: o site copia a mensagem e abre `whatsappLink` (link comercial), e a pessoa cola.
- `mensagemWhatsApp`: primeira linha da mensagem do formulário.
- `webhook`: endereço do webhook do Make que recebe os orçamentos (vazio = não envia).
- `locais`, `tamanhos`, `estilosForm`, `investimentos`: opções das caixas de seleção do formulário.

Ficam direto no HTML: textos do banner, e do "Quem sou", e o link do Instagram.

## Formulário de orçamento

Todos os campos são obrigatórios. Ao enviar, o formulário:

1. Manda os dados para o webhook do Make (`webhook` no objeto `site`), cada informação num campo separado: `nome`, `whatsapp`, `whatsapp_numero` (com 55), `local_do_corpo`, `tamanho`, `estilo`, `orcamento`, `ideia`, `data_envio` (padrão brasileiro, horário de Brasília: `22/10/2026 16:54:12`) e `pagina`.
2. Em seguida, leva a pessoa para o WhatsApp do Afonso com a mensagem do orçamento (já escrita, se `whatsappNumero` estiver preenchido; senão, copiada para colar).

No Make, use "Redetermine data structure" no módulo do webhook e envie um orçamento de teste pelo site publicado para o Make reconhecer os campos. O envio só funciona com o site publicado numa hospedagem; abrindo o arquivo direto do computador, alguns navegadores podem bloquear.

## Fotos

- `favicon.png` e `apple-touch-icon.png`: ícone do site com a foto do Afonso
- `assets/banner-2.webp`: foto do banner
- `assets/quem-sou-2.webp`: foto do "Quem sou"
- `assets/portfolio-15.webp` a `portfolio-29.webp`: fotos do portfólio

Cada foto do portfólio tem uma versão menor com `-480` no nome (por exemplo `portfolio-15-480.webp`), e o banner e o "Quem sou" têm `banner-2-800.webp` e `quem-sou-2-720.webp`. O celular carrega a versão menor e o computador a maior. Ao trocar uma foto, troque as duas versões.

## Desempenho

- As fontes do Google carregam sem bloquear a abertura da página.
- `_headers` (Netlify e Cloudflare Pages) e `vercel.json` (Vercel) mandam o navegador guardar as fotos em cache por 1 ano. Por isso, ao trocar uma foto, use um nome de arquivo novo (por exemplo `portfolio-15.webp`) em vez de substituir o arquivo com o mesmo nome. No GitHub Pages esses arquivos não têm efeito.
