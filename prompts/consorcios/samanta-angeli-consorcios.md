# 🏦 Prompt: Samanta Angeli - Consultoria de Consórcios

## 📋 Especificações Técnicas

**Objetivo:** Capturar leads qualificados de pessoas interessadas em adquirir bens através de consórcios

**Integração:** OpenAI GPT-4o obrigatória

**Tecnologias:** React + TypeScript + Tailwind CSS

---

## 🎯 PROMPT COMPLETO PARA BOLT.NEW

```
Crie uma página de captura completa para Samanta Angeli focada em pessoas que querem realizar sonhos através de consórcios.

OBJETIVO: Capturar leads qualificados de pessoas interessadas em adquirir bens através de consórcios

ESTRUTURA OBRIGATÓRIA:

Header: "Samanta Angeli - Consultoria Gratuita de Consórcios"
Hero: "Descubra como realizar seu sonho pagando até 40% menos que no financiamento"
Formulário com 5 perguntas específicas
CTA: "Descobrir Meu Consórcio Ideal"
Seção de resultado com análise personalizada
TEMA DE CORES: Azul corporativo (#1e40af), dourado (#f59e0b), branco

FORMULÁRIO (exatamente essas perguntas):

"Qual é o seu objetivo principal?"

Comprar meu primeiro carro
Trocar de veículo (upgrade)
Comprar imóvel próprio
Investir em imóvel para renda
"Qual valor você pretende investir?"

Até R$ 50.000
R$ 50.000 - R$ 150.000
R$ 150.000 - R$ 300.000
Acima de R$ 300.000
"Quanto você pode pagar mensalmente?"

Até R$ 500/mês
R$ 500 - R$ 1.500/mês
R$ 1.500 - R$ 3.000/mês
Acima de R$ 3.000/mês
"Qual sua urgência para ser contemplado?"

Preciso em até 6 meses
Posso aguardar até 1 ano
Tenho flexibilidade de prazo
Quero a menor parcela possível
"Conte mais sobre seu objetivo: qual bem deseja adquirir, finalidade de uso e situação financeira atual" (campo texto)

FUNCIONALIDADES:

Formulário responsivo
Validação de campos
Botão que simula "análise de consórcio"
Captura nome/email/whatsapp
Design moderno e conversivo
INTEGRAÇÃO OPENAI OBRIGATÓRIA:

Usar modelo gpt-4o
API Key configurada via .env (VITE_OPENAI_API_KEY)
FLUXO DE CAPTURA (OBRIGATÓRIO):
Quando clicar "Descobrir Meu Consórcio Ideal":

PRIMEIRO: Redirecionar para página/modal de captura com campos:

Nome Completo (obrigatório)
WhatsApp (obrigatório, com validação de formato)
E-mail (obrigatório, com validação)
Botão: "Gerar Análise Personalizada"
SEGUNDO: Após capturar dados, mostrar loading "Analisando seu perfil..."

TERCEIRO: Enviar para OpenAI com prompt personalizado incluindo o nome:

"Você é Samanta Angeli, consultora especializada em consórcios com 8 anos de experiência.
Analise o perfil de ${nomeCapturado}:

Nome: ${nomeCapturado}
WhatsApp: ${whatsapp}
Email: ${email}

Respostas do formulário:

Objetivo: ${resposta1}
Valor desejado: ${resposta2}
Capacidade mensal: ${resposta3}
Urgência: ${resposta4}
Descrição: ${resposta5}
Retorne JSON estruturado dirigindo-se diretamente ao ${nomeCapturado}:
{
"score_adequacao": 9.2,
"tipo_consorcio": "veículo/imóvel",
"modalidade_recomendada": "consórcio contemplado/não contemplado",
"recomendacoes": ["${nomeCapturado}, baseado no seu perfil, recomendo um consórcio de...", "Com sua capacidade de pagamento, sugiro...", "Para sua urgência, a melhor estratégia é..."],
"estrategia_contemplacao": ["Participar de lances mensais", "Aguardar sorteios naturais", "Considerar cotas contempladas"],
"comparativo_financiamento": {
"economia_total": "R$ 35.000",
"diferenca_juros": "18% menor que financiamento",
"prazo_sugerido": "80 meses"
},
"plano_personalizado": {
"valor_cota": "R$ 180.000",
"parcela_mensal": "R$ 1.200",
"taxa_administracao": "18%",
"tempo_estimado": "24 meses"
},
"resumo_executivo": "${nomeCapturado}, seu perfil é ideal para consórcio! Com base na sua capacidade financeira e objetivo, você pode economizar significativamente comparado ao financiamento tradicional..."
}"

VALIDAÇÕES OBRIGATÓRIAS:

Nome: mínimo 2 palavras
WhatsApp: formato brasileiro (XX) 9XXXX-XXXX ou (XX) XXXXX-XXXX
Email: formato válido
Não permitir análise sem captura completa
ARMAZENAMENTO:

Salvar dados capturados em localStorage/database
Enviar dados por email/webhook (opcional)
Tracking de conversão completa
EXIBIÇÃO DO RESULTADO:

Mostrar loading durante análise (3-5 segundos)
Exibir resultado formatado com cards visuais
Score em destaque (gauge/progress bar)
Recomendações em lista numerada
Comparativo visual com financiamento
CTA final: "Quero Falar com a Samanta Agora"
ESTRUTURA TÉCNICA OBRIGATÓRIA PARA BOLT.NEW:

Frontend: React + TypeScript + Tailwind CSS
Gerenciamento de estado: useState/useContext
API Routes: Criar /api/analyze-consortium.ts
Configuração: arquivo .env EXCLUSIVAMENTE com OPENAI_API_KEY
Tratamento de erros da API OpenAI
Estados de loading, sucesso e erro
Validação completa dos formulários
Componentes modulares e reutilizáveis
Design responsivo mobile-first
Animações e transições suaves
ARQUIVO .env (OBRIGATÓRIO):
Criar arquivo .env na raiz do projeto contendo APENAS:

OPENAI_API_KEY=sua-chave-da-api-aqui

IMPORTANTE: O arquivo .env deve conter EXCLUSIVAMENTE a variável OPENAI_API_KEY. Não incluir configurações de porta ou outras variáveis.

DEPENDÊNCIAS NECESSÁRIAS:

openai (para integração com GPT-4o)
react-hook-form (para validação de formulários)
lucide-react (para ícones)
clsx (para classes condicionais)
ELEMENTOS VISUAIS ESPECÍFICOS:

Ícones de carros, casas e calculadora
Testimonials de clientes satisfeitos
Selo de "Consultora Certificada"
Comparativo visual: Consórcio vs Financiamento
Timeline do processo de consórcio
COPY ESPECÍFICO PARA CONSÓRCIOS:

"Realize seu sonho sem comprometer o orçamento"
"Pague até 40% menos que no financiamento"
"Sem análise de crédito restritiva"
"Carência zero para usar o crédito"
"Consultoria especializada e gratuita"
Gere código completo, funcional e pronto para produção no ambiente Bolt.new.
```

---

## 📊 Métricas Esperadas

- **Taxa de Conversão:** 15-25%
- **Qualidade do Lead:** Alta (dados pessoais + análise personalizada)
- **Engajamento:** Análise AI aumenta tempo na página
- **Follow-up:** WhatsApp direto para conversão

## 🎨 Elementos Visuais

- Hero section impactante
- Formulário em etapas
- Loading com animação
- Cards de resultado
- Comparativo visual
- CTA destacado

## ⚙️ Configuração Técnica

1. Copie o prompt completo
2. Cole no Bolt.new
3. Aguarde a geração
4. Configure VITE_OPENAI_API_KEY no .env
5. Teste o fluxo completo

---

**Status:** ✅ Testado e validado
**Versão:** 1.0
**Última atualização:** Agosto 2025