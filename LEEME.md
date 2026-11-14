# Buscador Xurídico: versión independente para Netlify

É a mesma web que a de claude.ai, coas mesmas seccións: buscador (xurisprudencia, lexislación, definición e test), casos prácticos, explicar artigo, comparador, prazos e latinismos. Funciona sen claude.ai e calquera persoa pode usala sen conta.

A IA que hai detrás podes escollela ti:

| Opción | Custo | Diferenza |
|---|---|---|
| **Gemini (Google)** | Plan gratuíto con límites diarios | Non busca na web; no plan gratuíto Google pode usar os datos enviados para mellorar os seus produtos |
| **Claude (Anthropic)** | De pago, segundo o uso | Busca na web, así que a xurisprudencia e a lexislación saen máis actualizadas |

A **calculadora de prazos** e a lista de **latinismos** non usan IA: funcionan sempre e sen custo.

## Que hai na carpeta

| Ficheiro | Para que serve |
|---|---|
| `index.html` | A páxina |
| `netlify/edge-functions/ask.js` | O servidor: garda a clave en segredo e fala coa IA |
| `netlify.toml` | Configuración de Netlify |

## Paso 1: consegue unha clave

**Opción gratuíta (Gemini):**
1. Entra en **aistudio.google.com** coa túa conta de Google.
2. Preme **Get API key** e despois **Create API key**.
3. Copia a clave.

**Opción Claude:**
1. Entra en **console.anthropic.com**, engade saldo en *Billing* e pon un límite de gasto en *Limits*.
2. En *API Keys*, crea unha clave e cópiaa.

Non poñas nunca a clave dentro do `index.html`.

## Paso 2: sube a carpeta a GitHub

1. En **github.com**, crea un repositorio novo (por exemplo, `buscador-xuridico`).
2. Preme **uploading an existing file** e arrastra `index.html`, `netlify.toml`, `LEEME.md` e a carpeta `netlify` enteira.
3. Preme **Commit changes**. Comproba que aparece `netlify/edge-functions/ask.js`.

Se xa tiñas o repositorio da versión anterior, abonda con substituír eses ficheiros polos novos. Netlify publicará a nova versión el só.

## Paso 3: Netlify

1. En **netlify.com**, importa o repositorio desde GitHub (**Add new site → Import an existing project**) e preme **Deploy**.
2. En **Site configuration → Environment variables**, engade **unha** destas variables:
   - `GEMINI_API_KEY` = a túa clave de Google (opción gratuíta)
   - `ANTHROPIC_API_KEY` = a túa clave de Anthropic
3. En **Deploys**, preme **Trigger deploy → Deploy site** para que colla a clave.

**Non** arrastres a carpeta directamente a Netlify (Netlify Drop): así non se publica o servidor.

## Variables opcionais

| Variable | Para que serve |
|---|---|
| `AI_PROVIDER` | `gemini` ou `anthropic`, se configuraches as dúas claves |
| `GEMINI_MODEL` | Modelo de Gemini (por defecto `gemini-3-flash-preview`). Cámbiao se Google retira ese modelo |
| `MODEL_MAIN` / `MODEL_QUICK` | Modelos de Claude (por defecto `claude-sonnet-5-5` e `claude-haiku-5-5`) |

## Se algo falla

- **"O servidor non ten configurada ningunha clave":** falta a variable ou non volviches publicar despois de engadila.
- **"Chegouse ao límite gratuíto de Gemini":** usáronse as consultas gratuítas do día; espera ou cambia a Claude.
- **Un erro que menciona o modelo:** Google cambiou o nome do modelo. Pon o novo en `GEMINI_MODEL` (en aistudio.google.com ves os dispoñibles).
- **Erro 404 ao buscar:** a carpeta `netlify/edge-functions` non se subiu ben.

## Aviso

Os resultados xéraos unha IA. Pode equivocarse nun número de sentenza, nunha data ou na vixencia dunha norma, así que hai que comprobalos sempre na fonte oficial antes de citalos. A calculadora de prazos é orientativa: revisa os festivos autonómicos e locais.
