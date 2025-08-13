# 📝 Templates de Formulários para Landing Pages

## 🏦 Formulário Consórcios (5 Perguntas)

### Estrutura Base
```typescript
interface ConsortiumFormData {
  objetivo: string;
  valor: string;
  capacidadeMensal: string;
  urgencia: string;
  descricao: string;
}

interface UserData {
  nome: string;
  email: string;
  whatsapp: string;
}
```

### Perguntas Padrão - Consórcios

#### 1. Objetivo Principal
```json
{
  "pergunta": "Qual é o seu objetivo principal?",
  "tipo": "radio",
  "opcoes": [
    "Comprar meu primeiro carro",
    "Trocar de veículo (upgrade)", 
    "Comprar imóvel próprio",
    "Investir em imóvel para renda"
  ],
  "obrigatorio": true
}
```

#### 2. Valor de Investimento
```json
{
  "pergunta": "Qual valor você pretende investir?",
  "tipo": "radio",
  "opcoes": [
    "Até R$ 50.000",
    "R$ 50.000 - R$ 150.000",
    "R$ 150.000 - R$ 300.000", 
    "Acima de R$ 300.000"
  ],
  "obrigatorio": true
}
```

#### 3. Capacidade de Pagamento
```json
{
  "pergunta": "Quanto você pode pagar mensalmente?",
  "tipo": "radio", 
  "opcoes": [
    "Até R$ 500/mês",
    "R$ 500 - R$ 1.500/mês",
    "R$ 1.500 - R$ 3.000/mês",
    "Acima de R$ 3.000/mês"
  ],
  "obrigatorio": true
}
```

#### 4. Urgência
```json
{
  "pergunta": "Qual sua urgência para ser contemplado?",
  "tipo": "radio",
  "opcoes": [
    "Preciso em até 6 meses",
    "Posso aguardar até 1 ano", 
    "Tenho flexibilidade de prazo",
    "Quero a menor parcela possível"
  ],
  "obrigatorio": true
}
```

#### 5. Descrição Livre
```json
{
  "pergunta": "Conte mais sobre seu objetivo: qual bem deseja adquirir, finalidade de uso e situação financeira atual",
  "tipo": "textarea",
  "placeholder": "Ex: Quero comprar uma casa de 2 quartos para morar com minha família...",
  "maxLength": 500,
  "obrigatorio": true
}
```

## 🏠 Formulário Energia Solar (5 Perguntas)

#### 1. Tipo de Imóvel
```json
{
  "pergunta": "Qual tipo de imóvel você possui?",
  "tipo": "radio",
  "opcoes": [
    "Casa própria",
    "Apartamento próprio",
    "Empresa/Comércio",
    "Rural/Fazenda"
  ]
}
```

#### 2. Conta de Energia
```json
{
  "pergunta": "Qual o valor médio da sua conta de luz?",
  "tipo": "radio", 
  "opcoes": [
    "Até R$ 200/mês",
    "R$ 200 - R$ 500/mês",
    "R$ 500 - R$ 1.000/mês", 
    "Acima de R$ 1.000/mês"
  ]
}
```

#### 3. Motivação
```json
{
  "pergunta": "Qual sua principal motivação?",
  "tipo": "radio",
  "opcoes": [
    "Reduzir conta de luz",
    "Sustentabilidade ambiental",
    "Investimento no imóvel",
    "Independência energética"
  ]
}
```

#### 4. Urgência
```json
{
  "pergunta": "Quando pretende instalar?",
  "tipo": "radio",
  "opcoes": [
    "Nos próximos 3 meses",
    "Em até 6 meses",
    "No próximo ano", 
    "Apenas pesquisando"
  ]
}
```

#### 5. Orçamento
```json
{
  "pergunta": "Qual seu orçamento para o investimento?",
  "tipo": "radio",
  "opcoes": [
    "Até R$ 15.000",
    "R$ 15.000 - R$ 30.000",
    "R$ 30.000 - R$ 50.000",
    "Acima de R$ 50.000"
  ]
}
```

## 💼 Formulário Consultoria Empresarial

#### 1. Segmento
```json
{
  "pergunta": "Qual o segmento da sua empresa?",
  "tipo": "select",
  "opcoes": [
    "Comércio/Varejo",
    "Serviços", 
    "Indústria",
    "Tecnologia",
    "Saúde",
    "Educação",
    "Outro"
  ]
}
```

#### 2. Faturamento
```json
{
  "pergunta": "Qual o faturamento mensal aproximado?",
  "tipo": "radio",
  "opcoes": [
    "Até R$ 50.000",
    "R$ 50.000 - R$ 200.000", 
    "R$ 200.000 - R$ 500.000",
    "Acima de R$ 500.000"
  ]
}
```

## 📱 Validações JavaScript

### WhatsApp Brasileiro
```javascript
const validarWhatsApp = (numero) => {
  const regex = /^\(\d{2}\)\s?9?\d{4}-?\d{4}$/;
  return regex.test(numero);
};
```

### Email
```javascript
const validarEmail = (email) => {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
};
```

### Nome Completo
```javascript
const validarNome = (nome) => {
  return nome.trim().split(' ').length >= 2;
};
```

## 🎨 Estilos CSS (Tailwind)

### Card de Pergunta
```css
.question-card {
  @apply bg-white rounded-lg shadow-md p-6 mb-4;
}

.radio-option {
  @apply flex items-center p-3 border rounded-lg cursor-pointer hover:bg-blue-50 transition-colors;
}

.radio-option.selected {
  @apply bg-blue-100 border-blue-500;
}
```

### Botão CTA
```css
.cta-button {
  @apply bg-gradient-to-r from-blue-600 to-blue-700 text-white px-8 py-4 rounded-lg font-bold text-lg hover:shadow-lg transform hover:scale-105 transition-all;
}
```

---

**Templates testados e otimizados para conversão** ✅