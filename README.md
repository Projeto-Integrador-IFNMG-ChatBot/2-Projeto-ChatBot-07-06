RAG: Recuperação Aumentada por Geração (Retrieval-Augmented Generation)
Este projeto demonstra uma implementação simples de um sistema de Recuperação Aumentada por Geração (RAG), utilizando modelos de linguagem para extrair informações de documentos PDF e responder a perguntas de forma contextualizada. O foco é mostrar como combinar embeddings de texto para busca de similaridade (Retrieval) com a capacidade de um modelo de linguagem para gerar respostas (Generation).

🚀 Tecnologias Utilizadas
Python: Linguagem de programação principal.

PyMuPDF (fitz): Biblioteca para extrair texto de arquivos PDF.

Sentence-BERT (SBERT): Modelo de Hugging Face Transformers para gerar embeddings (vetores numéricos) de alta qualidade a partir de sentenças, preservando a similaridade semântica.

FAISS (Facebook AI Similarity Search): Biblioteca para busca eficiente de similaridade em vetores. É utilizada para encontrar os "chunks" (pedaços de texto) mais relevantes para uma determinada pergunta.

NumPy e scikit-learn: Utilizados para manipulação de vetores e normalização.

🧠 Como Funciona
O fluxo do projeto é dividido nas seguintes etapas:

Carregamento e Extração de Texto: O código carrega um arquivo PDF do Google Drive e extrai todo o seu conteúdo textual usando a biblioteca PyMuPDF.

Divisão em Chunks: O texto completo é dividido em pedaços menores (chunks). O código utiliza duas estratégias:

Divisão por Aspas: Extrai frases contidas entre aspas duplas, ideal para textos com citações ou sentenças bem delimitadas.

Divisão por Ponto Final: Separa o texto em sentenças, uma abordagem mais geral.

Criação de Embeddings: O modelo all-MiniLM-L6-v2 do SBERT é usado para converter cada chunk de texto em um vetor numérico. Esses vetores capturam o significado semântico do texto.

Indexação com FAISS: Os vetores dos chunks são indexados com o FAISS. Isso cria uma estrutura de dados otimizada para buscar rapidamente os vetores mais similares a um vetor de consulta.

Recuperação Aumentada: Quando uma pergunta é feita:

A pergunta é convertida em um vetor de embedding.

O FAISS é usado para encontrar os k chunks do PDF que possuem os embeddings mais similares ao da pergunta.

(A parte de "Geração" com um LLM, como o BLIP, que usaria esses chunks para formular a resposta, não está implementada neste notebook, mas o projeto estabelece a base para isso).

📊 Estrutura do Código
extrair_texto_pdf(PDF): Função para extrair texto e metadados de um PDF.

dividir_chunks_por_aspas(texto): Função para dividir o texto com base em aspas.

dividir_chunks_por_ponto_final(texto): Função para dividir o texto com base em pontos finais.

recuperar_top_k(pergunta, k): Função central que processa a pergunta, busca os chunks mais relevantes e retorna o texto e a similaridade.

Testes com PDFs: O código inclui exemplos de como testar o sistema com dois PDFs diferentes (PDF INSTITUICAO.pdf e PDF INSTITUCIONAL 2.pdf) e várias perguntas, demonstrando a funcionalidade de recuperação.

📝 Como Executar o Código
-Faça o upload dos arquivos PDF para o Google Drive.

-No Google Colab, execute as células para instalar as bibliotecas necessárias e montar o Google Drive.

-Aponte a variável PDF para o caminho do seu arquivo no Drive.

-Execute as células para extrair o texto, criar os chunks, gerar os embeddings e realizar os testes de similaridade.
