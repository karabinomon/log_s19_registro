# Registro da Semana 19 - Manipulação de Strings

**Escola Manoel Ignácio** - Desenvolvimento de Sistemas - 2ª série B - 2026  
**Lógica e Linguagem de Programação** - 3º Bimestre - Semana 19 - Aula 4  
`nome@dev:~$_`

---

## 🎯 Contexto e Objetivo

Nesta aula você aprenderá na prática os conceitos essenciais de **Manipulação de Strings**, métodos de divisão (`.split()`), busca (`.find()` / `in`) e técnicas profissionais de **Parsing de Logs** em Python para automação de triagem em ambientes de SOC (Security Operations Center) e DevOps.

Prove o seu conhecimento desenvolvendo um motor de análise em Python capaz de percorrer registros de logs brutos, identificar o nível de severidade de cada evento e destacar automaticamente apenas ocorrências críticas e erros.

---

## ⏳ Prazos e Pontuação

* **Entrega na 1ª semana (até 28 de agosto):** 10 pontos de semana AVA.
* **Entrega na 2ª semana (até 4 de setembro):** 5 pontos de semana AVA.
* **Entrega após 4 de setembro:** 1 ponto de semana AVA.

---

## ✈️ Envio e Comprovação

* **Identificação Obrigatória:** Insira seu **nome completo** e **turma** no cabeçalho do arquivo `triagem_logs.py` (no comentário no topo) e identifique-se no terminal antes de rodar o script.
* **Comprovação de Atividade:** Tire uma **captura de tela (screenshot)** nítida do seu VS Code exibindo o terminal com a execução do script e os alertas de segurança filtrados e formatados com o seu nome visível no código/terminal.
* **Opções de envio no AVA:** Envie a captura de tela acompanhada do arquivo `.py` ou o relatório em `.pdf` para a plataforma AVA.

---

## 🛠️ 1. Configuração Rápida no VS Code

### Passo 1: Arquivos do Projeto
Crie uma pasta no seu computador e abra-a no **VS Code**. Crie o seguinte arquivo na raiz:
```text
log_s19_registro_strings/
└── triagem_logs.py     # Script de parsing e automação de alertas
```

### Passo 2: Criando o Ambiente Virtual (.venv)
1. No VS Code, abra o arquivo `triagem_logs.py`.
2. No **canto inferior direito** da barra de status, clique na versão do Python (ou pressione `Ctrl+Shift+P` / `Cmd+Shift+P` e digite `Python: Create Environment`).
3. Escolha **Venv** e a versão do Python instalada.
4. Abra o terminal integrado (`Ctrl + \`` ou `Terminal > Novo Terminal`). Veja que o `(.venv)` estará ativo!

---

## 🔄 2. O que é Parsing de Logs e por que é essencial?

Um **log** é um registro cronológico de eventos gerado automaticamente por servidores, bancos de dados e aplicações. Cada linha de log é uma string estruturada com delimitadores como pipes (`|`), espaços ou vírgulas.

O **parsing de logs** é o processo de decompor essas strings brutas em dados úteis usando:
- **Divisão por delimitador (`.split()`):** Fragmenta a linha em campos individuais (data, nível, serviço, IP, mensagem).
- **Limpeza (`.strip()` e `.replace()`):** Remove espaços residuais e prefixos desnecessários.
- **Filtragem (`in` e condicionais):** Isola eventos de severidade alta para análise imediata.

---

## 💻 3. Código Inicial: A Base de Logs Brutos

Copie o código abaixo para o arquivo `triagem_logs.py`.

### 📄 `triagem_logs.py` (Estrutura Inicial)

```python
# ==========================================================
# Identificação do Estudante:
# Nome Completo: [SEU NOME COMPLETO AQUI]
# Turma: 2ª Série B - DS - 2026
# Disciplina: Lógica e Linguagem de Programação (Semana 19 - Aula 4)
# ==========================================================

"""Módulo de triagem e parsing de logs de segurança."""

# Lista de logs brutos simulando a extração de um servidor real
logs_brutos = [
    "2024-07-15 08:42:17 | ERROR | auth-service | ip=192.168.4.21 | Login failed: invalid credentials",
    "2024-07-15 08:43:02 | INFO  | api-gateway  | ip=10.0.0.5     | Request completed: 200 OK",
    "2024-07-15 08:43:45 | WARN  | db-connector | ip=10.0.1.12    | Connection pool at 87% capacity",
    "2024-07-15 08:44:10 | ERROR | auth-service | ip=192.168.4.21 | Login failed: invalid credentials",
    "2024-07-15 08:46:30 | CRITICAL | firewall  | ip=192.168.4.21 | Port scan detected: 1024 ports/5s"
]

def analisar_logs(registros: list):
    """Realiza o parsing e filtra apenas eventos de severidade ERROR ou CRITICAL."""
    print("Iniciando a varredura dos logs de segurança...\n")
    
    # 🎯 TODO: O estudante deve implementar o parsing aqui
    pass

if __name__ == "__main__":
    analisar_logs(logs_brutos)
```

---

## 🔍 4. Passo a Passo: Desenvolvendo o Motor de Parsing

### 1. Fatiando os campos com `.split("|")`
Cada registro possui 5 campos divididos por pipe:
- Índice `0`: Data e hora (`2024-07-15 08:42:17`)
- Índice `1`: Nível de severidade (`ERROR`, `INFO`, `WARN`, `CRITICAL`)
- Índice `2`: Serviço de origem (`auth-service`)
- Índice `3`: Endereço IP (`ip=192.168.4.21`)
- Índice `4`: Mensagem do evento (`Login failed: invalid credentials`)

---

### 2. Implementando a Filtragem e Formatação
Substitua o conteúdo da função `analisar_logs` pela lógica de triagem:

```python
def analisar_logs(registros: list):
    print("Iniciando a varredura dos logs de segurança...\n")
    
    for linha in registros:
        # Divide a linha pelos pipes e limpa os espaços em branco de cada campo
        partes = [campo.strip() for campo in linha.split("|")]
        
        nivel = partes[1]
        ip = partes[3].replace("ip=", "")
        mensagem = partes[4]
        
        # Filtra apenas registros críticos ou com erro
        if "ERROR" in nivel or "CRITICAL" in nivel:
            print(f"⚠️ ALERTA DE SEGURANÇA! Nível: [{nivel}] | Origem: [{ip}] | Mensagem: [{mensagem}]")
```

---

## 🎯 5. Mão na Massa do Estudante: Execução e Validação

### Missão do Estudante:
1. Complete a função no arquivo `triagem_logs.py`.
2. No terminal integrado, execute o script:
   ```bash
   python triagem_logs.py
   ```
3. Verifique se a saída no console exibiu exatamente os 3 alertas de segurança (`ERROR`, `ERROR` e `CRITICAL`), ignorando os eventos `INFO` e `WARN`.

---

## 📸 6. Comprovante para Envio no AVA

Para validar sua entrega:
1. Certifique-se de que preencheu seu **Nome Completo** no topo de `triagem_logs.py`.
2. Execute no terminal:
   ```bash
   python triagem_logs.py
   ```
3. Tire uma captura de tela mostrando o código e o resultado no terminal com os alertas de segurança gerados.
4. Envie a captura de tela no AVA dentro do prazo para garantir sua pontuação!

---

## 📌 7. Resumo dos Comandos e Métodos Úteis (Cheat Sheet)

### Métodos de Strings Utilizados:
| Método / Operador | O que faz? | Exemplo de Uso |
| :--- | :--- | :--- |
| `.split(separador)` | Divide a string em uma lista de elementos com base no delimitador. | `linha.split("\|")` |
| `.strip()` | Remove espaços em branco antes e depois do texto. | `campo.strip()` |
| `.replace(antigo, novo)` | Substitui um trecho do texto por outro (ex: remove `ip=`). | `campo.replace("ip=", "")` |
| `operador in` | Verifica se um texto está contido dentro da string. | `"ERROR" in nivel` |
