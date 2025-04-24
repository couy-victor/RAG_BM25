# 🔍 RAG Híbrido: Combinando BM25 e Embeddings para Consultas à LGPD

Este projeto implementa um sistema de Recuperação Aumentada de Geração (RAG) híbrido para consultas sobre a Lei Geral de Proteção de Dados (LGPD) do Brasil, combinando a precisão léxica do algoritmo BM25 com a compreensão semântica de embeddings vetoriais.

## 📋 Visão Geral

O sistema permite consultas em linguagem natural sobre a LGPD, retornando respostas precisas com referências aos trechos relevantes da lei. A abordagem híbrida supera as limitações de métodos individuais:

- **Embeddings vetoriais**: Excelente compreensão semântica, mas pode falhar com termos técnicos raros
- **BM25**: Ótima correspondência léxica, mas limitada em compreensão contextual
- **Abordagem híbrida**: Combina os pontos fortes de ambas as técnicas

## 🚀 Funcionalidades

- Extração e processamento automático do texto da LGPD a partir de PDF
- Indexação dual (vetorial via ChromaDB e estatística via BM25)
- Busca híbrida com ponderação configurável entre métodos
- Interface interativa para consultas em linguagem natural
- Respostas detalhadas com citação de fontes e nível de confiança

## 🛠️ Tecnologias Utilizadas

- **Sentence Transformers**: Para geração de embeddings semânticos
- **ChromaDB**: Para armazenamento e busca vetorial
- **Rank-BM25**: Implementação eficiente do algoritmo BM25
- **PyPDF**: Para extração de texto de documentos PDF
- **Pydantic-AI**: Framework para construção de agentes de IA

## 🔧 Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/rag-bm25-lgpd.git
   cd rag-bm25-lgpd
   ```

2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure as variáveis de ambiente (opcional):
   ```bash
   cp .env.example .env
   # Edite o arquivo .env conforme necessário
   ```

## 📊 Arquitetura do Sistema

O sistema implementa o fluxo RAG moderno com estas etapas:

1. **Ingestão**: Extração de texto do PDF da LGPD e divisão em chunks controlados
2. **Indexação**: Armazenamento dual (vetorial via ChromaDB e estatístico via BM25)
3. **Recuperação Híbrida**: Busca paralela em ambos os índices com fusão ponderada de resultados
4. **Geração Aumentada**: Uso dos contextos recuperados para geração de respostas precisas
5. **Apresentação**: Formatação clara com metadados de confiança e fontes

## 💻 Uso

Execute o script principal para iniciar uma sessão interativa:

```bash
python RAG_BM25.py
```

Ou importe o sistema em seu próprio código:

```python
from RAG_BM25 import LGPDRagSystem
import asyncio

async def main():
    system = LGPDRagSystem()
    await system.initialize()
    response = await system.ask("Quais são os direitos do titular de dados?")
    print(response.answer)

asyncio.run(main())
```

## 📘 Notebook Explicativo

O repositório inclui um notebook Jupyter (`descricacao_rag_bm25.ipynb`) que explica em detalhes:

- Comparação entre técnicas de busca (Similaridade de Cossenos vs. BM25)
- Vantagens da abordagem híbrida
- Boas práticas implementadas no código
- Arquitetura detalhada do sistema

## 🔄 Parâmetros Configuráveis

O sistema pode ser personalizado através de variáveis de ambiente:

- `PDF_PATH`: Caminho para o arquivo PDF da LGPD
- `CHROMA_DB_DIR`: Diretório para persistência do ChromaDB
- `EMBEDDING_MODEL`: Modelo de embedding a ser utilizado
- `LLM_MODEL_NAME`: Modelo de linguagem para geração de respostas
- `HYBRID_ALPHA`: Peso para balancear embeddings vs BM25 (0-1)
- `TOP_K`: Número de documentos a recuperar
- `CHUNK_SIZE`: Tamanho dos chunks de texto
- `CHUNK_OVERLAP`: Sobreposição entre chunks consecutivos

## 📝 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para detalhes.

## 👥 Autores

Desenvolvido pela Equipe Scoras Academy.

---

## 📊 Comparação de Técnicas de Busca

| Característica | Similaridade de Cossenos | BM25 | Abordagem Híbrida |
|---------------|-------------------------|------|-------------------|
| Base matemática | Álgebra linear | Teoria da informação | Combinação ponderada |
| Captação semântica | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| Correspondência exata | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Tratamento de termos raros | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Sensibilidade a contexto | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
