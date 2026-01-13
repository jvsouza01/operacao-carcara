# 🧪 Guia de Teste Local - Operação Carcara

## Pré-requisitos

- Python 3.7+ instalado
- Navegador web

## Passo a Passo

### 1. Instalar Dependências

Abra o terminal na pasta do projeto e execute:

```powershell
cd c:\Users\jao_v\Desktop\operacao_carcara\operacao_carcara
pip install -r requirements.txt
```

### 2. Iniciar o Servidor Local

```powershell
python app.py
```

Você verá:
```
⚠️  Usando SQLite local para testes: mentoria_local.db
 * Running on http://127.0.0.1:5000
```

### 3. Criar as Tabelas no Banco

Abra o navegador e acesse:

```
http://127.0.0.1:5000/_iniciar_banco_de_dados_uma_vez
```

Isso criará as tabelas de alunos, registros, empresas, simulados, etc.

### 4. Criar a Tabela de Logs (Nova Funcionalidade)

```
http://127.0.0.1:5000/_migrar_logs_delecao
```

Você verá: `"Tabela de logs de deleção criada com sucesso!"`

### 5. Testar a Aplicação

1. **Página principal (Rankings)**:
   ```
   http://127.0.0.1:5000/
   ```

2. **Registrar Questões** (onde está a nova funcionalidade):
   ```
   http://127.0.0.1:5000/registrar-questoes
   ```

## 🧪 Testando o Sistema de Logs de Deleção

### Teste 1: Bloquear Deleção sem Aluno Selecionado

1. Vá em `/registrar-questoes`
2. **NÃO** selecione nenhum aluno no dropdown
3. Tente clicar em "Apagar" em algum registro
4. ✅ Deve aparecer: `"Você precisa selecionar seu nome antes de apagar um registro!"`

### Teste 2: Criar Log de Deleção

1. **Selecione seu nome** no dropdown (ex: "Alan vitor")
2. Adicione um registro de teste (50 questões, 40 acertos)
3. Clique em "Apagar" no registro que você acabou de criar
4. ✅ Deve aparecer na lista:
   ```
   Alan vitor apagou: Alan vitor - 40 acertos de 50 questões
   ```
   (em vermelho e itálico, SEM botão "Apagar")

### Teste 3: Verificar Persistência

1. Adicione mais alguns registros
2. Apague alguns (com aluno selecionado)
3. Recarregue a página (F5)
4. ✅ Os logs de deleção devem continuar aparecendo

## 🛑 Parar o Servidor

No terminal onde o servidor está rodando:
- Pressione `Ctrl + C`

## 📁 Arquivos Gerados

Após rodar localmente, você verá:
- `mentoria_local.db` - Banco SQLite local (não fazer commit!)

## 🚀 Quando Subir para Produção

1. Configure a variável de ambiente `DATABASE_URL` com a URL do PostgreSQL
2. Acesse `/_migrar_logs_delecao` em produção
3. O resto funciona automaticamente!

## ⚠️ Observações

- **SQLite é apenas para testes locais**
- O banco local é criado vazio (sem dados pré-existentes)
- Os alunos padrão serão criados ao acessar `/_iniciar_banco_de_dados_uma_vez`
