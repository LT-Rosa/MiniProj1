# MiniProj1 — Tarefa 2.2 | Programação Web Avançada

**SPA de currículo vitae**, desenvolvida com Vue.js 3 e Vite. Uma única página HTML (`index.html`) serve de entrada. O Vue apresenta dinamicamente cada secção sem recarregar o documento.

## Requisitos do enunciado

| Requisito | Onde está implementado |
|---|---|
| Quem sou eu? | Menu e vista `perfil` em `src/App.vue` |
| O que faço? | Menu e vista `experiencia` em `src/App.vue` |
| Hobbies | Menu e vista `interesses` em `src/App.vue` |
| SPA / navegação interna | `activePage`, `navigateTo`, fragmentos `#` e eventos de histórico |
| Rodapé com identidade virtual | `socialLinks` em `src/App.vue` (preencher URLs pessoais) |
| Framework Vue.js | `src/main.js`, `src/App.vue` |
| Wireframe | `docs/wireframe.pdf` |
| Repositório Git `MiniProj1` | Criar/publicar com esse nome |

## Instalar e executar no Visual Studio Code

Requer Node.js compatível com o `package.json`. Abrir a pasta do projeto e executar:

```bash
npm ci
npm run dev
```

Abrir o endereço apresentado pelo Vite, normalmente `http://localhost:5173/`.

Não abras `index.html` diretamente pelo explorador de ficheiros: o código Vue é carregado como módulos e precisa do servidor Vite. No VS Code, também podes selecionar **Launch Chrome against localhost** e premir F5; a configuração inicia o servidor e abre a aplicação.

Para gerar a versão de publicação:

```bash
npm run build
```

O resultado fica em `dist/`. O código-fonte e o projeto Vite devem permanecer no repositório; `node_modules`, `dist` e `.git` não são incluídos no ZIP de entrega.

## Personalização obrigatória antes da entrega

- Confirmar os dados de formação, datas e descrição da experiência.
- Confirmar o endereço de correio eletrónico.
- Substituir os valores `href: ''` em `socialLinks` por URLs reais dos perfis pretendidos. Os ícones só surgem depois de configuradas as ligações, para não enviar o utilizador para páginas genéricas.
- Rever as competências e os hobbies.

## Fundamentação

- MDN, *Your first website*: planeamento, HTML, CSS, JavaScript e publicação.
- Segue Technologies, *What is a Single Page Application?*: interface dinâmica numa única página.
- Red Gate, *Introduction to Vue.js with a Single Page Application*: conceitos Vue e SPA.
- TestDriven.io, *Developing a Single Page App with FastAPI and Vue.js*: exemplo de aplicação Vue. **Não foi implementada API**, pois o currículo não necessita de back-end.

## Entrega

1. Criar repositório Git chamado `MiniProj1` e enviar o código.
2. Incluir `docs/wireframe.pdf` e este README.
3. Submeter na plataforma os ficheiros produzidos e um ficheiro com a ligação ao repositório (modelo: `docs/LINK_REPOSITORIO.txt`).
4. Participar no fórum da tarefa, conforme solicitado no enunciado.
