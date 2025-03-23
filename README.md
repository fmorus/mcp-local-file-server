# MCP Local File Server

Servidor para acessar e manipular arquivos locais usando MCP (Managed Control Panel).

## Instalação

1. Clone o repositório:
```bash
git clone https://github.com/fmorus/mcp-local-file-server.git
cd mcp-local-file-server
```

2. Instale as dependências:
```bash
npm install
```

3. Inicie o servidor:
```bash
npm start
```

O servidor estará rodando em `http://localhost:3000`

## API Endpoints

### Listar Arquivos
- **GET** `/files?dir={diretório}`
- Lista todos os arquivos em um diretório
- O parâmetro `dir` é opcional (padrão: diretório atual)

### Ler Arquivo
- **GET** `/file?path={caminho_do_arquivo}`
- Lê o conteúdo de um arquivo

### Upload de Arquivo
- **POST** `/file`
- Faz upload de um arquivo
- Use `multipart/form-data` com o campo `file`

### Atualizar Arquivo
- **PUT** `/file`
- Atualiza o conteúdo de um arquivo
- Body: `{ "path": "caminho_do_arquivo", "content": "novo_conteudo" }`

### Deletar Arquivo
- **DELETE** `/file?path={caminho_do_arquivo}`
- Remove um arquivo ou diretório

## Exemplo de Uso

```javascript
// Listar arquivos
fetch('http://localhost:3000/files')
  .then(response => response.json())
  .then(files => console.log(files));

// Ler arquivo
fetch('http://localhost:3000/file?path=/caminho/do/arquivo.txt')
  .then(response => response.json())
  .then(data => console.log(data.content));

// Upload de arquivo
const formData = new FormData();
formData.append('file', arquivoParaUpload);
fetch('http://localhost:3000/file', {
  method: 'POST',
  body: formData
});

// Atualizar arquivo
fetch('http://localhost:3000/file', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    path: '/caminho/do/arquivo.txt',
    content: 'Novo conteúdo'
  })
});

// Deletar arquivo
fetch('http://localhost:3000/file?path=/caminho/do/arquivo.txt', {
  method: 'DELETE'
});
```

## Segurança

⚠️ **Atenção**: Este servidor tem acesso total aos arquivos do sistema. Use com cautela e apenas em ambientes confiáveis.