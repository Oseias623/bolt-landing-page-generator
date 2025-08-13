# ⚙️ Configuração OpenAI para Bolt.new

## 🔑 API Key Setup

### 1. Obter API Key OpenAI
1. Acesse [platform.openai.com](https://platform.openai.com)
2. Faça login em sua conta
3. Vá em **API Keys** no menu
4. Clique em **Create new secret key**
5. Copie a chave gerada

### 2. Configurar no Projeto Bolt.new

#### Arquivo .env (OBRIGATÓRIO)
Crie na raiz do projeto:

```env
VITE_OPENAI_API_KEY=sk-sua-chave-aqui
```

**⚠️ IMPORTANTE:** 
- Use APENAS `VITE_OPENAI_API_KEY`
- Não adicione outras variáveis
- Prefixo `VITE_` é obrigatório no Bolt.new

### 3. Instalação de Dependências

```bash
npm install openai
```

### 4. Exemplo de Uso na API Route

```typescript
// /api/analyze-consortium.ts
import OpenAI from 'openai';

const openai = new OpenAI({
  apiKey: import.meta.env.VITE_OPENAI_API_KEY,
});

export async function POST(request: Request) {
  try {
    const { formData, userData } = await request.json();
    
    const completion = await openai.chat.completions.create({
      model: "gpt-4o",
      messages: [
        {
          role: "system",
          content: "Você é Samanta Angeli, consultora especializada em consórcios..."
        },
        {
          role: "user", 
          content: `Analise o perfil: ${JSON.stringify({formData, userData})}`
        }
      ],
      temperature: 0.7,
      max_tokens: 2000,
      response_format: { type: "json_object" }
    });

    return new Response(completion.choices[0].message.content, {
      headers: { 'Content-Type': 'application/json' }
    });
    
  } catch (error) {
    console.error('Erro OpenAI:', error);
    return new Response(
      JSON.stringify({ error: 'Erro na análise' }), 
      { status: 500 }
    );
  }
}
```

### 5. Hook React para Chamada API

```typescript
// hooks/useAnalyzeConsortium.ts
import { useState } from 'react';

interface AnalysisResult {
  score_adequacao: number;
  tipo_consorcio: string;
  recomendacoes: string[];
  // ... outros campos
}

export const useAnalyzeConsortium = () => {
  const [loading, setLoading] = useState(false);
  const [result, setResult] = useState<AnalysisResult | null>(null);
  const [error, setError] = useState<string | null>(null);

  const analyze = async (formData: any, userData: any) => {
    setLoading(true);
    setError(null);
    
    try {
      const response = await fetch('/api/analyze-consortium', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ formData, userData })
      });
      
      if (!response.ok) throw new Error('Erro na análise');
      
      const data = await response.json();
      setResult(data);
    } catch (err) {
      setError('Erro ao processar análise');
    } finally {
      setLoading(false);
    }
  };

  return { analyze, loading, result, error };
};
```

## 🔄 Fluxo Completo

1. **Formulário** → Coleta respostas
2. **Captura** → Nome, email, WhatsApp  
3. **API Call** → OpenAI GPT-4o
4. **Resultado** → JSON estruturado
5. **Exibição** → Interface visual

## 🛡️ Tratamento de Erros

```typescript
// Validações de segurança
if (!import.meta.env.VITE_OPENAI_API_KEY) {
  throw new Error('API Key OpenAI não configurada');
}

// Rate limiting
const MAX_REQUESTS_PER_MINUTE = 10;

// Fallback para falhas
const fallbackResponse = {
  score_adequacao: 8.5,
  tipo_consorcio: "Análise temporariamente indisponível",
  recomendacoes: ["Entre em contato para análise personalizada"]
};
```

## 📊 Monitoramento

- **Logs de uso** da API
- **Taxa de sucesso** das análises  
- **Tempo de resposta** médio
- **Custos** da OpenAI por análise

---

**Custo estimado:** ~$0.02 por análise com GPT-4o