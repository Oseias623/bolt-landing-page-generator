# ⚡ Guia de Boas Práticas para Bolt.new

## 🎯 Estrutura de Prompts Eficazes

### ✅ Elementos Obrigatórios

1. **Objetivo Claro**: "Crie uma página de captura para..."
2. **Tecnologia Específica**: "React + TypeScript + Tailwind CSS"
3. **Funcionalidades Detalhadas**: Formulários, validações, API calls
4. **Design System**: Cores, tipografia, componentes
5. **Fluxo de Usuário**: Passo a passo detalhado

### 📝 Template de Prompt Base

```
Crie uma [TIPO DE PÁGINA] para [PERSONA] focada em [OBJETIVO].

OBJETIVO: [Descrição específica do objetivo]

ESTRUTURA OBRIGATÓRIA:
- Header: [Texto específico]
- Hero: [Proposta de valor]
- Formulário: [X perguntas específicas]
- CTA: [Texto do botão]
- Resultado: [Tipo de análise/retorno]

TEMA DE CORES: [Cores específicas com hex codes]

FUNCIONALIDADES:
- [Lista detalhada de funcionalidades]

INTEGRAÇÃO [API] OBRIGATÓRIA:
- [Configurações específicas]

FLUXO [DETALHADO]:
- [Cada step do usuário]

VALIDAÇÕES:
- [Regras de validação]

ESTRUTURA TÉCNICA:
- [Tecnologias e arquitetura]

DEPENDÊNCIAS:
- [Lista de bibliotecas necessárias]
```

## 🛠️ Configurações Técnicas

### Arquivo .env Correto
```env
# ✅ CORRETO para Bolt.new
VITE_OPENAI_API_KEY=sk-sua-chave

# ❌ EVITAR no Bolt.new
PORT=3000
REACT_APP_API_URL=http://localhost
```

### Dependências Recomendadas
```json
{
  "openai": "^4.x.x",
  "react-hook-form": "^7.x.x", 
  "lucide-react": "^0.x.x",
  "clsx": "^2.x.x",
  "@hookform/resolvers": "^3.x.x",
  "zod": "^3.x.x"
}
```

## 🎨 Design System Padrão

### Paleta de Cores
```css
/* Primárias */
--blue-600: #2563eb;
--blue-700: #1d4ed8;
--gold-500: #f59e0b;
--gold-600: #d97706;

/* Neutras */
--gray-50: #f9fafb;
--gray-100: #f3f4f6;
--gray-800: #1f2937;
--gray-900: #111827;

/* Status */
--green-500: #10b981;
--red-500: #ef4444;
--yellow-500: #eab308;
```

### Componentes Base
```typescript
// Button Component
interface ButtonProps {
  variant: 'primary' | 'secondary' | 'ghost';
  size: 'sm' | 'md' | 'lg';
  loading?: boolean;
  children: React.ReactNode;
  onClick?: () => void;
}

// Card Component  
interface CardProps {
  title?: string;
  children: React.ReactNode;
  className?: string;
}

// Form Field Component
interface FormFieldProps {
  label: string;
  error?: string;
  required?: boolean;
  children: React.ReactNode;
}
```

## 📱 Responsividade

### Breakpoints Tailwind
```css
/* Mobile First */
.container {
  @apply px-4 mx-auto;
}

/* sm: 640px */
@screen sm {
  .container { @apply px-6; }
}

/* md: 768px */  
@screen md {
  .container { @apply px-8; }
}

/* lg: 1024px */
@screen lg {
  .container { @apply max-w-6xl px-8; }
}
```

### Layout Responsivo
```typescript
// Mobile: Stack vertical
// Desktop: Grid 2 colunas
<div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
  <div>Formulário</div>
  <div>Informações</div>
</div>
```

## 🔄 Estados da Aplicação

### Loading States
```typescript
const [loading, setLoading] = useState(false);
const [error, setError] = useState<string | null>(null);
const [success, setSuccess] = useState(false);

// Loading UI
{loading && (
  <div className="flex items-center justify-center p-8">
    <div className="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-600"></div>
    <span className="ml-2">Analisando...</span>
  </div>
)}
```

### Error Handling
```typescript
try {
  const result = await apiCall(data);
  setSuccess(true);
} catch (error) {
  setError('Erro ao processar. Tente novamente.');
  console.error('API Error:', error);
}
```

## 🎯 Otimizações de Conversão

### Formulários Progressivos
```typescript
const [currentStep, setCurrentStep] = useState(1);
const totalSteps = 5;

// Progress Bar
<div className="w-full bg-gray-200 rounded-full h-2">
  <div 
    className="bg-blue-600 h-2 rounded-full transition-all"
    style={{ width: `${(currentStep / totalSteps) * 100}%` }}
  />
</div>
```

### CTAs Persuasivos
```typescript
const ctaTexts = {
  initial: "Descobrir Meu Perfil",
  loading: "Analisando...", 
  success: "Ver Minha Análise",
  final: "Quero Falar com Consultor"
};
```

### Validação em Tempo Real
```typescript
// React Hook Form + Zod
const schema = z.object({
  nome: z.string().min(3, "Nome deve ter pelo menos 3 caracteres"),
  email: z.string().email("Email inválido"),
  whatsapp: z.string().regex(/^\(\d{2}\)\s9\d{4}-\d{4}$/, "WhatsApp inválido")
});
```

## 📊 Analytics e Tracking

### Eventos de Conversão
```typescript
// GTM / GA4 Events
const trackEvent = (eventName: string, parameters: object) => {
  if (typeof window !== 'undefined' && window.gtag) {
    window.gtag('event', eventName, parameters);
  }
};

// Uso
trackEvent('form_submit', { form_type: 'lead_capture' });
trackEvent('analysis_complete', { user_score: 8.5 });
```

### Funil de Conversão
1. **Visualização** da página
2. **Início** do formulário  
3. **Conclusão** do formulário
4. **Captura** de dados pessoais
5. **Análise** completada
6. **CTA final** clicado

## ⚠️ Erros Comuns no Bolt.new

### ❌ Evitar
```typescript
// Imports incorretos
import fs from 'fs'; // Node.js não funciona

// Variáveis de ambiente erradas  
process.env.OPENAI_API_KEY // ❌ 
import.meta.env.OPENAI_API_KEY // ❌

// APIs Server-side complexas
app.use(express.json()); // ❌
```

### ✅ Usar
```typescript
// Imports corretos
import { useState, useEffect } from 'react';
import OpenAI from 'openai';

// Variáveis de ambiente
import.meta.env.VITE_OPENAI_API_KEY // ✅

// APIs simples
export async function POST(request: Request) { // ✅
  // Lógica da API
}
```

## 🚀 Prompt Otimizado Final

### Checklist Pré-Geração
- [ ] Objetivo claro definido
- [ ] Persona específica
- [ ] Formulário com perguntas exatas
- [ ] Cores em hex codes
- [ ] Fluxo step-by-step
- [ ] Integrações especificadas
- [ ] Validações detalhadas
- [ ] Dependências listadas
- [ ] Design responsivo
- [ ] Estados de loading/erro

---

**Seguindo estas práticas, você terá 90%+ de sucesso na geração** 🎯