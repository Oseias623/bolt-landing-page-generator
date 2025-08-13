# 🚀 Bolt Landing Page Generator

## Prompts e Templates para Gerar Landing Pages no Bolt.new

Repositório com prompts otimizados para criar landing pages de alta conversão usando Bolt.new com integração OpenAI.

### 📁 Estrutura do Repositório

```
bolt-landing-page-generator/
├── prompts/
│   ├── consorcios/
│   │   └── samanta-angeli-consorcios.md
│   ├── energia-solar/
│   ├── consultoria/
│   └── ecommerce/
├── templates/
│   ├── formularios/
│   ├── capturas/
│   └── componentes/
├── configuracoes/
│   ├── openai-setup.md
│   └── bolt-config.md
└── README.md
```

### 🎯 Prompts Disponíveis

#### 🏦 Consórcios
- **Samanta Angeli - Consultoria de Consórcios**
  - Localização: `prompts/consorcios/samanta-angeli-consorcios.md`
  - Integração: OpenAI GPT-4o
  - Captura: 5 perguntas + dados pessoais
  - Análise: Personalizada com JSON estruturado

### 🛠️ Como Usar

1. **Escolha o prompt** adequado ao seu nicho
2. **Copie o conteúdo** do arquivo .md
3. **Cole no Bolt.new** e execute
4. **Configure a API Key** OpenAI no .env
5. **Customize** conforme necessário

### ⚙️ Configurações Necessárias

#### OpenAI API Key
```env
VITE_OPENAI_API_KEY=sua-chave-aqui
```

#### Dependências Comuns
- openai
- react-hook-form
- lucide-react
- clsx

### 📊 Métricas de Conversão

- **Taxa de preenchimento** do formulário inicial
- **Taxa de captura** de dados pessoais
- **Qualidade dos leads** gerados
- **Engajamento** com análise personalizada

### 🎨 Padrões de Design

- **Cores:** Azul corporativo + Dourado + Branco
- **Layout:** Mobile-first responsivo
- **UX:** Fluxo de captura em etapas
- **Validações:** Campos obrigatórios com feedback

### 📱 Compatibilidade

- ✅ Bolt.new
- ✅ React + TypeScript
- ✅ Tailwind CSS
- ✅ OpenAI API
- ✅ Mobile responsivo

---

**Desenvolvido para maximizar conversões e qualificar leads de alta qualidade** 🎯