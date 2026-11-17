# Flyers do Germinar

Gerador de flyers do **Espaço Germinar** (Juazeiro do Norte – CE). É uma página web em um único arquivo (`index.html`). A pessoa escreve os textos, escolhe as cores e os desenhos e baixa uma imagem PNG pronta para o WhatsApp, o Instagram ou para imprimir.

A página não precisa de servidor, de instalação nem de conta: tudo roda no navegador.

## Como usar

1. Abra o `index.html` no navegador (Chrome, Edge, Firefox ou Safari, no computador ou no celular).
2. Siga os passos do formulário, de cima para baixo. A prévia ao lado muda enquanto você digita.
3. Toque em **Baixar imagem**.

Campos deixados em branco não aparecem no flyer. O que você digitou fica guardado no aparelho (`localStorage`), mesmo se fechar a página.

## Passos do formulário

| Passo | O que faz |
|---|---|
| 1 · Modelo | Carrega um modelo com textos de exemplo: *Colônia de férias*, *Matrículas*, *Evento*, *Aviso aos pais*, *Reunião de pais* ou *Em branco*. **Trocar de modelo apaga os textos já digitados.** |
| 2 · Título | Frase de chamada (pequena, acima), primeira parte do título e parte colorida (destaque). O título diminui sozinho para caber em até 3 linhas. |
| 3 · Lista do quadro branco | Título da lista, um item por linha e uma frase final opcional. Com 5 itens ou mais, a lista passa a ter 2 colunas. Sem título e sem itens, o quadro não aparece. |
| 4 · Datas e informações | **Caixa laranja** (destaque: rótulo, informação principal e aviso extra) e **caixa branca** (rótulo e informação). A caixa que ficar vazia some do flyer. |
| 5 · Contato | Texto da faixa verde do rodapé (telefone, Instagram, endereço). |
| 6 · Tamanho, cores e letra | Formato, paleta e fonte (veja as tabelas abaixo). |
| 7 · Desenhos e enfeites | Até 2 desenhos pequenos, 1 desenho grande, enfeite de fundo e estilo do quadro. O botão **Sortear** escolhe uma combinação nova sem mexer nos textos nem nas cores. |
| 8 · Fotos e logo | Troca ou remove o logo do canto superior e permite enviar uma foto ou ilustração própria, que ocupa o lugar do desenho grande. PNG com fundo transparente fica melhor. |

### Formatos

| Opção | Tamanho exportado |
|---|---|
| Post do Instagram (em pé) | 1080 × 1350 px |
| Quadrado (Instagram e WhatsApp) | 1080 × 1080 px |
| Status do WhatsApp / Story | 1080 × 1920 px |
| Folha A4 para imprimir | 2160 × 3054 px (exportado em resolução dobrada) |

### Paletas

Todas usam as cores do logo: azul `#0066CA`, verde-terra `#006634`, verde-folha `#03CA33` e laranja-semente `#FB6201`.

- **Germinar**: céu azul-claro, destaques em laranja
- **Broto**: fundo verde-claro
- **Semente**: fundo laranja-claro
- **Céu azul**: fundo azul forte com título branco

### Fontes

Moderna (Poppins, padrão), Arredondada e infantil (Baloo 2), Divertida (Fredoka) e Mais séria (Montserrat). As fontes vêm do Google Fonts. A Poppins também está embutida no arquivo, para funcionar sem internet.

### Desenhos e enfeites

- **Desenhos (adesivos):** Sol, Pipa, Balões, Livros, Lápis, Artes, Estrela, Nuvem, Arco-íris, Borboleta, Flor, Música, Pipoca, Bola, Mandacaru e Coração. Todos são desenhados em código, sem arte de terceiros, e ganham contorno branco e sombra, como um adesivo.
- **Enfeite do fundo:** Folhinhas, Confete, Estrelinhas, Nuvens, Bolinhas ou Sem enfeite.
- **Quadro branco:** Simples, Título numa faixa colorida ou Com borda tracejada.

## Download

O nome do arquivo é gerado a partir do título, por exemplo `germinar-a-nossa-colonia-de-ferias.png`.

- **Navegador comum:** a imagem é baixada para a pasta Downloads (no celular, para a galeria ou os arquivos).
- **Dentro de um iframe** (onde o download direto costuma ser bloqueado): abre uma janela com a imagem para salvar com "toque e segure" ou com o botão direito.
- **Dentro do Claude** (artifact): usa a permissão `downloads` do ambiente quando ela está disponível.

## Detalhes técnicos

- **Arquivo único:** HTML, CSS e JavaScript puros, sem dependências nem etapa de build. O logo e a fonte Poppins estão embutidos em base64, por isso o arquivo tem cerca de 480 KB.
- **Desenho:** tudo é desenhado num `<canvas>` com 1080 px de largura. A função `drawFit` tenta escalas de 100% até 56% e usa a primeira em que o conteúdo cabe no formato escolhido.
- **Aleatoriedade estável:** a posição dos enfeites usa um gerador com semente (`S.seed`). O mesmo flyer sai sempre igual, e o botão Sortear só troca a semente.
- **Armazenamento local:**
  - `germinar-flyer-v1`: textos e escolhas
  - `germinar-flyer-v1-logo`: logo personalizado
  - `germinar-flyer-v1-art`: foto enviada

  Se a imagem for grande demais para o `localStorage`, ela continua no flyer, mas some quando a página é recarregada (a página avisa).
- **Acessibilidade:** botões com `aria-pressed`, avisos em região `aria-live`, foco visível e tema claro/escuro automático.
- **Responsivo:** em telas de até 860 px, a prévia fica acima do formulário.

## Como alterar

Tudo fica no `<script>` do `index.html`:

| Para mudar… | Edite |
|---|---|
| Modelos e textos de exemplo | `EX` |
| Paletas de cores | `P` |
| Formatos e tamanhos | `FM` |
| Texto padrão do rodapé | `FOOT` |
| Desenhos (adesivos) | `ST` (cada um tem um nome `n` e uma função de desenho `f(c, s)`) |
| Enfeites de fundo | `BG` e a função `pattern` |
| Estilos do quadro | `CARD` |
| Logo padrão | constante `LOGO` (data URI) |

Se mudar a estrutura dos dados salvos, troque o valor de `KEY` (por exemplo, para `germinar-flyer-v2`). Assim, dados antigos guardados no aparelho não quebram a página.
