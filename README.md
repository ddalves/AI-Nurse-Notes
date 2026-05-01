##AI-Nurse-Notes 🩺🤖##
Protótipo de IA (MVP) para validação técnica de registros de enfermagem, integrando as normas do COFEN e diferenciando competências entre Enfermeiros e Técnicos.

#Sobre o Projeto#
Este projeto nasce da necessidade de melhorar a precisão e a legalidade dos registros de enfermagem em prontuários de saúde. Utilizando modelos de linguagem de larga escala (LLM), o sistema atua como um revisor em tempo real, transformando anotações informais em registros técnicos padronizados.

#Diferenciais Técnicos e Legais#
O grande diferencial deste protótipo é a integração da Lei do Exercício Profissional. O sistema identifica o perfil do usuário para aplicar filtros de competência:

Perfil Técnico/Auxiliar: Foco em Anotação de Enfermagem (sinais observáveis, queixas e procedimentos executados). O sistema restringe o uso de termos privativos da função.

Perfil Enfermeiro: Foco em Evolução de Enfermagem, permitindo terminologia propedêutica complexa e exame físico completo.

#Tecnologias Utilizadas#

Python: Linguagem base para o desenvolvimento da lógica.

Google Gemini 1.5 Flash: Modelo de IA generativa para o processamento de linguagem natural.

PyPDF2: Biblioteca para extração de contexto técnico a partir de documentos PDF (Guia de Anotações do COFEN).

Pandas: Futura implementação para análise de dados assistenciais estruturados.

#Estrutura do Repositório#

prototipo_NurseAi.ipynb: Notebook com a lógica de execução e prompts estruturados.

Enviando por email anotacao-de-enfermagem.pdf: Base de conhecimento normativa utilizada pela IA.

#Próximos Passos#

Implementação de interface visual (Streamlit).

Expansão da base de dados para incluir protocolos específicos.

Refinamento de RAG (Retrieval-Augmented Generation) para consultas normativas mais profundas.
