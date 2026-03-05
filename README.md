# Ecommerce-Project-Final

Cómo funciona

El proyecto sigue la arquitectura clásica de un sistema RAG + Agent:

1. Ingesta de datos

Se carga un catálogo de productos desde un archivo estructurado (CSV o JSON).

Cada producto contiene información como:

nombre del producto

precio

rating

descripción

características

Estos datos se transforman en texto estructurado para poder ser indexados.

2. Vectorización

Los productos se convierten en embeddings semánticos usando el modelo:

text-embedding-3-small

Los embeddings se almacenan en una base de datos vectorial alojada en:

Chroma Cloud.

Esto permite realizar búsquedas semánticas rápidas sobre miles de productos.

3. Retrieval

Cuando el usuario hace una pregunta, el sistema:

Convierte la consulta en embeddings

Busca los productos más similares en la base vectorial

Recupera los top K resultados más relevantes

Esto se implementa mediante un Retriever de LangChain.

4. Generación

El contexto recuperado se envía a un modelo de lenguaje:

GPT-4o-mini

El LLM genera una respuesta que incluye:

recomendaciones de productos

precio

rating

explicación breve

Esto se realiza con un pipeline RAG de LangChain.

🤖 Chatbot Ecommerce Agent

El sistema también incluye un agente conversacional construido con:

LangChain

Este agente permite a los usuarios interactuar con el ecommerce como si fuera un asistente de compras.

Funcionalidades del agente

El agente puede:

buscar productos

recomendar productos

añadir productos al carrito

mostrar el carrito

guardar dirección de envío

procesar pagos simulados

🛒 Herramientas del agente (Tools)

El agente utiliza varias tools para interactuar con el sistema.

Buscar productos

Permite consultar el catálogo mediante búsqueda semántica.

buscar_producto(query)

Utiliza el pipeline RAG para devolver recomendaciones relevantes.

Ver carrito

Muestra los productos actualmente añadidos.

ver_carrito()
Añadir producto al carrito

Permite añadir productos al carrito de compra.

agregar_producto(title, price)
Guardar dirección de envío

Permite guardar la información del cliente.

guardar_direccion(nombre, email, direccion)
Pago con tarjeta (simulado)

Simula el pago del carrito.

pagar_tarjeta(nombre, numero, mes, año, cvc)

Calcula el total y confirma la compra.

🧠 Ejemplo de uso

El usuario puede realizar preguntas como:

“¿Qué chaquetas de montaña tienen mejor valoración?”

“Recomiéndame botas de trekking por menos de 150€”

“¿Qué mochilas son buenas para senderismo?”

“Añade la mochila Osprey al carrito”

“Muéstrame mi carrito”

“Quiero pagar mi pedido”

El sistema responde con:

recomendaciones relevantes

precio

rating

descripción breve

🔒 Guardrails (control de dominio)

El sistema incluye guards para evitar preguntas fuera del dominio del ecommerce.

Si el usuario pregunta algo como:

“Ayúdame a escribir un script en Python”

El sistema responde:

“Este asistente solo puede ayudar con consultas sobre productos y compras en el ecommerce.”

Esto evita que el chatbot se desvíe de su función principal.

📊 Observabilidad con LangSmith

El proyecto integra:

LangSmith

Esto permite:

monitorizar ejecuciones del RAG

analizar prompts y respuestas

medir latencia

ver tokens usados

detectar errores

evaluar calidad de respuestas

Cada consulta genera un trace completo del pipeline.

🌐 Deployment

El chatbot puede desplegarse con:

Gradio

Esto permite crear una interfaz web interactiva donde los usuarios pueden chatear con el agente.

También se puede usar:

Streamlit

APIs backend

integración con WhatsApp o Webchat

🛠️ Tecnologías utilizadas

Python

LangChain

OpenAI API

Chroma Cloud (Vector Database)

LangSmith

Gradio

Streamlit

CSV / JSON Product Dataset

📦 Arquitectura del proyecto
ecommerce-agent/

data/
   products.csv
   products.json

notebooks/
   rag_experiments.ipynb
   agent_testing.ipynb

src/
   ingest.py
   rag_pipeline.py
   agent_tools.py
   guards.py

app/
   gradio_app.py

config/
   chroma_config.py
   env_variables.py
⚙️ Pipeline simplificado
User Question
      ↓
Retriever (Chroma Cloud)
      ↓
Top K Products
      ↓
Prompt Template
      ↓
GPT-4o-mini
      ↓
Product Recommendation
