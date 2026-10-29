### A) Paleta (P1–P5)

Use **Inspect** no Figma (Alt+Shift+I) para tirar os hex exatos. Cada paleta tem:

- uma **cor escura**: títulos, rodapé, faixa da chamada, card "Serra";
- uma **cor de destaque**: botão principal, ícone da marca, borda dos passos;
- **três cores de selo**: "Últimas vagas", "Novo" e "Iniciante";
- **quatro tons claros**: fundo do hero e dos cards de roteiro;
- fundo da página, texto comum, texto secundário e bordas.

Escreva os hex direto nas regras (os valores abaixo são só exemplo; use os do seu frame):

```css
body {
  background: #f5f5f5; /* fundo da página */
  color: #222222; /* texto comum */
}
.btn--principal {
  background: #ffcc00; /* cor de destaque */
  color: #333333; /* cor escura */
}
```

Usar variáveis (`:root { --cor-escura: #333333; }` e depois `var(--cor-escura)`) é opcional.

### B) Tipografia (T1–T5)

Pares possíveis:

| ID  | Display (títulos) | UI (texto comum) |
| --- | ----------------- | ---------------- |
| T1  | Bebas Neue        | Work Sans        |
| T2  | Young Serif       | Instrument Sans  |
| T3  | Space Grotesk     | Space Grotesk    |
| T4  | Anton             | Karla            |
| T5  | Zilla Slab        | Source Sans 3    |

As fontes já estão no HTML. Você só declara:

```css
body {
  font-family: "Work Sans", sans-serif;
}
h1,
h2,
h3 {
  font-family: "Bebas Neue", sans-serif;
}
```

Confira no Inspect o tamanho e o peso (`font-weight`) de cada texto: eles mudam de um par para outro.

### C) Ordem das seções (S1–S5)

O HTML está sempre na ordem `hero → roteiros → saidas → passos → chamada → inscricao → depoimentos`. O seu Figma pode mostrar outra sequência. O hero é sempre o primeiro.

**Reordene com `order:` no flexbox, sem mexer no HTML.** O `main` precisa ser `display: flex; flex-direction: column;`:

```css
main {
  display: flex;
  flex-direction: column;
}
main > [data-section="hero"] {
  order: 0;
}
main > [data-section="saidas"] {
  order: 1;
}
main > [data-section="roteiros"] {
  order: 2;
}
main > [data-section="chamada"] {
  order: 3;
}
main > [data-section="passos"] {
  order: 4;
}
main > [data-section="inscricao"] {
  order: 5;
}
main > [data-section="depoimentos"] {
  order: 6;
}
```

### D) Densidade (D1–D5)

A densidade muda paddings e gaps. **Os valores já vêm em pixels no seu Figma**: use o Inspect e copie. Densidades possíveis: D1 Compacto · D2 Regular · D3 Conforto · D4 Amplo · D5 Arejado.

Os frames estão em auto layout, então o Inspect mostra o padding e o gap de cada caixa. O gap do `main` é o espaço entre uma seção e outra.

## Layout

A página tem 1440 px de largura no Figma, com o conteúdo numa coluna central de **1200 px**. Reproduza esse desktop; não precisa de versão para celular.

Tudo se monta com flexbox e grid:

- **Topo, botões, lista de próximas saídas e chamada:** flexbox.
- **Hero:** grid de 2 colunas (texto e card "Próxima saída"), com a faixa de números ocupando a linha de baixo inteira.
- **Roteiros:** grid com `grid-template-areas`. O card "Serra" ocupa duas linhas e "Noturna" ocupa duas colunas.
- **Como funciona e Inscrição:** grid de 2 colunas (texto à esquerda, conteúdo à direita).
- **Depoimentos e rodapé:** grid de colunas.

## Requisitos técnicos

1. **Não altere o HTML.**
2. **`order:`** no `main` para a ordem das seções do seu frame.
3. **Grid** nos roteiros, com `grid-template-areas`.
4. **Estados interativos:** `:hover` em botões, links do menu e linhas da lista de saídas; `:focus-visible` em botões, links e campos do formulário, com contorno visível.

## Critérios de avaliação (10 pontos)

| Pontos | Critério                                                                                |
| ------ | --------------------------------------------------------------------------------------- |
| 5,0    | Fidelidade visual ao Figma: cores, fontes, tamanhos, espaçamentos e alinhamentos        |
| 3,0    | Layout com flexbox e grid, `order:` na ordem certa e `grid-template-areas` nos roteiros |
| 1,0    | Estados `:hover` e `:focus-visible`                                                     |
| 1,0    | CSS válido e organizado                                                                 |

Valide o CSS em [jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator/) (_By file upload_; avisos não contam).

## Dicas

- **Comece pelas cores e fontes**: o resto encaixa mais rápido.
- A marca "Passo Alto", os ícones e os emojis **já estão no HTML**. Você só estiliza (`.saida__emoji`, por exemplo, para tamanho e fundo).
- **Não reorganize o HTML.** Use `order:` no flexbox para a ordem das seções.
- O Inspect do Figma mostra os valores em pixels prontos: use direto, sem fazer contas.
- Use `outline: 1px solid red` provisório para ver as caixas. Tire antes de entregar.
- O Figma está em 1440 px de largura. Confira no navegador com zoom em 100% e janela larga.

## Snippet de partida

Cole este bloco no início do seu `styles.css` e vá preenchendo os valores conforme você inspeciona o seu Figma. Os comentários com `/* ← */` marcam o que muda de acordo com a sua variação.

```css
/* =========================================================================
   Passo Alto — styles.css
   Nome: ____________  RM: ______  Frame: vNN
   ========================================================================= */

/* ----------  Base  ---------- */
body {
  font-family: "...", sans-serif; /* ← fonte UI do seu par            */
  background: #ffffff; /* ← fundo da página                */
  color: #000000; /* ← texto comum                    */
}

h1,
h2,
h3 {
  font-family: "...", sans-serif; /* ← fonte display do seu par       */
  color: #000000; /* ← cor escura                     */
}

main {
  display: flex;
  flex-direction: column;
  gap: 100px; /* ← espaço entre as seções         */
}

main > section {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

/* ----------  Ordem das seções (S?) — troque conforme o seu Figma  ---------- */
main > [data-section="hero"] {
  order: 0;
}
main > [data-section="roteiros"] {
  order: 1;
}
main > [data-section="saidas"] {
  order: 2;
}
main > [data-section="passos"] {
  order: 3;
}
main > [data-section="chamada"] {
  order: 4;
}
main > [data-section="inscricao"] {
  order: 5;
}
main > [data-section="depoimentos"] {
  order: 6;
}

/* ----------  A partir daqui é com você  ----------
   Sugestão de ordem para implementar:
   1. .topo, .marca e .menu
   2. .btn e variações (--principal, --contorno, --escuro, --pequeno, --largo)
   3. .hero (.hero__titulo, .destaque, .numeros)
   4. .cabecalho (título + texto de cada seção)
   5. .roteiros__grade + .roteiro
   6. .saidas__lista + .saida + .selo
   7. .passos + .passo
   8. .chamada
   9. .inscricao + .ficha, .campo, .grupo, .opcao
   10. .depoimentos__grade + .depoimento
   11. .rodape (colunas + marca gigante)
*/
```
