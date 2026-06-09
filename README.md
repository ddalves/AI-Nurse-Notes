<div align="center">

<img src="https://github.com/user-attachments/assets/c8ff0047-8d4b-4eee-9cad-987f462c55f8" width="120" alt="NurseAI Logo"/>

# NurseNotesAI — Revisor de Registros de Enfermagem

**Transformando anotações informais em registros técnicos, legais e padronizados com IA generativa e RAG.**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Gemini](https://img.shields.io/badge/Google_Gemini-2.5_Flash-4285F4?style=flat-square&logo=google&logoColor=white)](https://ai.google.dev)
[![COFEN](https://img.shields.io/badge/Normas-COFEN-00897B?style=flat-square)](https://cofen.gov.br)
[![Status](https://img.shields.io/badge/Status-MVP-orange?style=flat-square)]()
[![License](https://img.shields.io/badge/Licença-MIT-green?style=flat-square)](LICENSE)

</div>

---

## 🩺 O Problema

Registros de enfermagem imprecisos ou fora dos padrões técnicos e legais representam um risco real: responsabilização jurídica do profissional, falhas na continuidade do cuidado e auditoria comprometida. A correção manual é lenta e sujeita a inconsistências.

**NurseNotesAI** resolve isso automaticamente — em segundos.

---

## 💡 O que é o NurseNotesAI?

Um revisor de prontuário baseado em **LLM + RAG** que:

- Recebe uma anotação de enfermagem em linguagem informal ou com desvios técnicos
- Recupera as normas aplicáveis diretamente do **Guia de Anotações do COFEN** (via busca semântica)
- Devolve um registro **técnico, legal e padronizado** — diferenciando o perfil do profissional

---

## ⚖️ Diferencial Legal: Competências por Perfil

O grande diferencial do projeto é a integração da **Lei do Exercício Profissional de Enfermagem**. O sistema aplica filtros automáticos de competência conforme o perfil informado:

| Perfil | Tipo de Registro | Terminologia Permitida |
|--------|-----------------|----------------------|
| 👨‍⚕️ **Técnico / Auxiliar** | Anotação de Enfermagem | Sinais observáveis, queixas, procedimentos executados. Termos privativos bloqueados. |
| 👩‍⚕️ **Enfermeiro** | Evolução de Enfermagem | Exame físico completo, terminologia propedêutica, raciocínio diagnóstico. |

---

## 🏗️ Arquitetura RAG

```
PDF do COFEN
     │
     ▼
┌─────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Chunking   │────▶│  text-embedding  │────▶│  Cache em disco │
│  (overlap)  │     │  (Gemini API)    │     │  (.json)        │
└─────────────┘     └──────────────────┘     └─────────────────┘
                                                      │
                          Anotação do usuário          │
                                │                     ▼
                                ▼             ┌───────────────┐
                    ┌───────────────────┐     │  Similaridade │
                    │  Query Embedding  │────▶│  de Cosseno   │
                    └───────────────────┘     └───────┬───────┘
                                                      │ Top-K chunks
                                                      ▼
                                             ┌─────────────────┐
                                             │  Gemini 1.5     │
                                             │  Flash (LLM)    │
                                             └────────┬────────┘
                                                      │
                                                      ▼
                                          Registro técnico corrigido
```

---

## 🚀 Como Usar

### Pré-requisitos

```bash
pip install numpy PyPDF2 google-generativeai
```

### Configuração

1. Clone o repositório
2. Adicione sua **Google AI API Key** na Célula 2 do notebook
3. Coloque o PDF `Enviando por email anotacao-de-enfermagem.pdf` na pasta do projeto

### Execução

Execute as células do notebook `rag_enfermagem.ipynb` **em ordem**:

```
Célula 1 → Instalação
Célula 2 → Configuração da API
Células 3–5 → Definição das funções
Célula 6 → Indexação do PDF (com cache automático)
Célula 7 → Funções do simulador
Célula 8 → ✅ Uso interativo
```

> **💾 Cache inteligente:** os embeddings são salvos em `cache_embeddings.json`. A partir da segunda execução, o PDF não é reprocessado — zero custo adicional de API.

### Exemplo de uso

```
Você é:
  1 - Técnico de Enfermagem
  2 - Enfermeiro
Digite 1 ou 2: 1

Digite a anotação para corrigir:
> paciente com barriga estufada, falando que tá com dor e não conseguiu fazer xixi hoje

────────────────────────────────────────────────────
Sugestão: Paciente refere dor abdominal e relata ausência de micção nas últimas [X] horas.
Abdome apresenta-se distendido à inspeção. Enfermeiro responsável comunicado.

Por que: Substitui linguagem informal por terminologia técnica compatível com as
competências do técnico de enfermagem, conforme Resolução COFEN nº 564/2017.
────────────────────────────────────────────────────
```

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|-----------|-----|
| **Python 3.10+** | Linguagem base |
| **Google Gemini 2.5 Flash** | Geração e correção do registro |
| **Gemini text-embedding** | Vetorização semântica dos chunks |
| **PyPDF2** | Extração de texto do PDF do COFEN |
| **NumPy** | Cálculo de similaridade de cosseno |
| **JSON** | Cache persistente de embeddings |

---

## 📁 Estrutura do Repositório

```
📦 projeto_enfermagem_ia/
├── 📓 rag_enfermagem.ipynb          # Notebook principal
├── 📄 Enviando por email anotacao-de-enfermagem.pdf    # Base normativa (COFEN)
├── 💾 cache_embeddings.json         # Cache gerado automaticamente
└── 📋 README.md
```

---

## 🗺️ Roadmap

- [x] MVP com RAG e diferenciação de perfis
- [x] Cache de embeddings para economia de tokens
- [ ] Interface visual com **Streamlit**
- [ ] Expansão da base normativa (protocolos específicos por especialidade)
- [ ] Histórico de correções com exportação para PDF
- [ ] API REST para integração com sistemas de prontuário eletrônico
- [ ] Suporte a múltiplos documentos normativos (ANVISA, CFM)

---

## ⚠️ Aviso Legal

Este projeto é um **protótipo acadêmico/educacional**. As sugestões geradas pela IA não substituem o julgamento clínico do profissional de saúde habilitado nem a consulta direta à legislação vigente. O uso em ambiente clínico real requer validação especializada.

---

<div align="center">

Desenvolvido com 🩺 e ☕ para melhorar a qualidade dos registros de enfermagem no Brasil.

</div>
