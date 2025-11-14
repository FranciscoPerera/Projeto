# Endereçador

Endereçador é uma aplicação web simples para gerar etiquetas de remessa com dados do remetente e do destinatário. O projeto facilita o preenchimento de endereços a partir do CEP (ViaCEP), mantém um histórico local de CEPs e permite gerar um PDF pronto para impressão usando html2canvas + jsPDF.

Logo: `img/logo.png`

## Principais funcionalidades

- Preenchimento de remetente e destinatário (nome, telefone, endereço, número, complemento, bairro, cidade, UF, CEP).
- Busca de endereço pelo CEP usando a API ViaCEP.
- Histórico local de CEPs (armazenado em localStorage) com opção de selecionar entradas antigas ou limpar o histórico.
- Validações básicas (CEP, UF, telefone e campos obrigatórios).
- Máscaras para CEP e telefone.
- Pré-visualização da etiqueta no próprio site.
- Geração de PDF com a etiqueta posicionada de forma compacta (usa html2canvas e jsPDF).
- Notificações visuais e feedback ao usuário (sucesso/erro).

## Tecnologias / Bibliotecas

- HTML / CSS / JavaScript (vanilla)
- html2canvas (CDN) — captura a pré-visualização como imagem
- jsPDF (CDN) — gera o PDF com a imagem da etiqueta
- API de CEP: ViaCEP (https://viacep.com.br)

As bibliotecas são carregadas via CDN diretamente em `index.html`:
- https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js
- https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js

## Como usar (em 2 minutos)

1. Abra o arquivo `index.html` no navegador (ou rode um servidor local).
   - Para rodar rápido via Python:  
     ```bash
     python -m http.server 8000
     # e acesse http://localhost:8000
     ```
2. Preencha os dados do remetente e do destinatário.
3. Nos campos de CEP, digite o CEP (8 dígitos). O app tentará preencher rua, bairro, cidade e UF automaticamente via ViaCEP.
4. Ajuste número e complemento, confirme os dados na pré-visualização.
5. Clique em "Gerar PDF" para criar a etiqueta como um PDF pronto para impressão. O PDF será gerado e baixado/aberto em nova aba.

## Configurações importantes (onde ajustar)

No arquivo `index.html` há um objeto de configuração (const CONFIG) com valores úteis:

- STORAGE_KEY: chave usada no localStorage para salvar o histórico de CEPs (ex.: `cep_history_v2`).
- MAX_HISTORY_ITEMS: quantidade máxima de entradas no histórico (ex.: `50`).
- API_ENDPOINTS: endpoints usados para buscar CEP.
  - Por padrão usa ViaCEP: `https://viacep.com.br/ws/${cep}/json/`.
  - Existe também um placeholder para `correios` (com proxy) caso queira adicionar um fallback.

Se quiser adicionar outro provedor como fallback, edite o método de busca em `CepAPI.fetch` dentro de `index.html`.

## Validações e máscaras

- Validações:
  - CEP: 8 dígitos (formato `#####-###` ou apenas números).
  - UF: duas letras maiúsculas.
  - Telefone: validação simples para formatos brasileiros.
  - Campos obrigatórios: nome, rua, número, bairro, cidade, UF, CEP (conforme campo).
- Máscaras:
  - CEP e telefone são formatados automaticamente enquanto você digita.

## Histórico de CEP

- Histórico salvo no localStorage sob a chave configurada.
- Ao preencher o campo CEP, é possível abrir um dropdown com CEPs buscados anteriormente e reutilizá-los.
- Há opção de limpar o histórico direto no dropdown.

## Estrutura do projeto

- index.html — página principal com todo o HTML/CSS/JS incorporado.
- img/ — pasta com imagens (ex.: logo).
- LICENSE — arquivo de licença do repositório.

## Desenvolvimento

- Projeto é estático; editar `index.html` é suficiente para alterar comportamento ou layout.
- Para desenvolvimento local, use um servidor local (ex.: `python -m http.server`) para evitar bloqueios de CORS ao testar fetchs externos.
- Se precisar de um proxy para acessar APIs que exigem CORS (ex.: API dos Correios), adapte `CONFIG.API_ENDPOINTS.correios` e implemente um proxy server.

## Contribuições

Contribuições são bem-vindas. Para sugerir melhorias:
- Abra uma issue descrevendo a sugestão ou bug encontrado.
- Envie pull requests com mudanças pequenas e descrições claras.

## Observações e melhorias futuras sugeridas

- Adicionar fallback real para outro provedor de CEP além do ViaCEP.
- Suporte a múltiplas etiquetas por página e layout configurável.
- Exportar configurações do usuário (por exemplo, exportar/ importar histórico de CEP).
- Internacionalização (i18n) caso queira suporte a outros idiomas.

## Licença

Veja o arquivo `LICENSE` para detalhes sobre a licença do projeto.

---
Feito com base no comportamento e nas funcionalidades implementadas em `index.html`. Se quiser, atualizo o README com mais detalhes (ex.: exemplos de uso avançado, screenshots ou instruções de deploy).
