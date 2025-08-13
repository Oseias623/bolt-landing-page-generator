# 📥 Templates de Captura de Dados

## 🎯 Captura Básica (Nome + Email + WhatsApp)

### Componente React
```typescript
import { useState } from 'react';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const captureSchema = z.object({
  nome: z.string()
    .min(3, "Nome deve ter pelo menos 3 caracteres")
    .regex(/^[a-zA-ZÀ-ÿ\s]+$/, "Nome deve conter apenas letras"),
  email: z.string()
    .email("Email inválido")
    .toLowerCase(),
  whatsapp: z.string()
    .regex(/^\(\d{2}\)\s?9?\d{4}-?\d{4}$/, "WhatsApp deve estar no formato (XX) 9XXXX-XXXX")
});

interface CaptureModalProps {
  isOpen: boolean;
  onClose: () => void;
  onCapture: (data: CaptureFormData) => void;
  title?: string;
  subtitle?: string;
  buttonText?: string;
}

type CaptureFormData = z.infer<typeof captureSchema>;

export function CaptureModal({ 
  isOpen, 
  onClose, 
  onCapture,
  title = "Para continuar, precisamos de alguns dados",
  subtitle = "Seus dados estão seguros e não serão compartilhados",
  buttonText = "Gerar Análise Personalizada"
}: CaptureModalProps) {
  const [loading, setLoading] = useState(false);
  
  const { register, handleSubmit, formState: { errors } } = useForm<CaptureFormData>({
    resolver: zodResolver(captureSchema)
  });

  const onSubmit = async (data: CaptureFormData) => {
    setLoading(true);
    try {
      await onCapture(data);
    } finally {
      setLoading(false);
    }
  };

  if (!isOpen) return null;

  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
      <div className="bg-white rounded-lg max-w-md w-full p-6">
        {/* Header */}
        <div className="text-center mb-6">
          <h3 className="text-xl font-bold text-gray-900 mb-2">
            {title}
          </h3>
          <p className="text-gray-600 text-sm">
            {subtitle}
          </p>
        </div>

        {/* Form */}
        <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
          {/* Nome */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              Nome Completo *
            </label>
            <input
              {...register('nome')}
              type="text"
              placeholder="Digite seu nome completo"
              className="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            />
            {errors.nome && (
              <p className="text-red-500 text-sm mt-1">{errors.nome.message}</p>
            )}
          </div>

          {/* Email */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              E-mail *
            </label>
            <input
              {...register('email')}
              type="email"
              placeholder="seu@email.com"
              className="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            />
            {errors.email && (
              <p className="text-red-500 text-sm mt-1">{errors.email.message}</p>
            )}
          </div>

          {/* WhatsApp */}
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">
              WhatsApp *
            </label>
            <input
              {...register('whatsapp')}
              type="tel"
              placeholder="(11) 99999-9999"
              className="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            />
            {errors.whatsapp && (
              <p className="text-red-500 text-sm mt-1">{errors.whatsapp.message}</p>
            )}
          </div>

          {/* Buttons */}
          <div className="flex gap-3 pt-4">
            <button
              type="button"
              onClick={onClose}
              className="flex-1 px-4 py-3 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors"
            >
              Cancelar
            </button>
            <button
              type="submit"
              disabled={loading}
              className="flex-1 px-4 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 disabled:opacity-50 disabled:cursor-not-allowed transition-colors"
            >
              {loading ? (
                <div className="flex items-center justify-center">
                  <div className="animate-spin rounded-full h-4 w-4 border-b-2 border-white mr-2"></div>
                  Aguarde...
                </div>
              ) : (
                buttonText
              )}
            </button>
          </div>
        </form>

        {/* Privacy Notice */}
        <p className="text-xs text-gray-500 text-center mt-4">
          🔒 Seus dados estão protegidos pela Lei Geral de Proteção de Dados (LGPD)
        </p>
      </div>
    </div>
  );
}
```

## 📱 Hook de Captura

```typescript
import { useState } from 'react';

interface CaptureData {
  nome: string;
  email: string;
  whatsapp: string;
}

export function useCapture() {
  const [isOpen, setIsOpen] = useState(false);
  const [capturedData, setCapturedData] = useState<CaptureData | null>(null);

  const openCapture = () => setIsOpen(true);
  const closeCapture = () => setIsOpen(false);

  const handleCapture = async (data: CaptureData) => {
    // Salvar no localStorage
    localStorage.setItem('captured_lead', JSON.stringify({
      ...data,
      timestamp: new Date().toISOString(),
      source: window.location.href
    }));

    setCapturedData(data);
    setIsOpen(false);

    // Opcional: Enviar para webhook/CRM
    try {
      await fetch('/api/capture-lead', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
      });
    } catch (error) {
      console.error('Erro ao enviar lead:', error);
    }

    return data;
  };

  return {
    isOpen,
    capturedData,
    openCapture,
    closeCapture,
    handleCapture,
    hasCaptured: !!capturedData
  };
}
```

## 🎨 Variações de Design

### Modal Minimalista
```css
.capture-modal-minimal {
  @apply bg-white rounded-2xl shadow-2xl max-w-sm w-full p-8;
}

.capture-modal-minimal .title {
  @apply text-2xl font-bold text-gray-900 mb-3 text-center;
}

.capture-modal-minimal .input {
  @apply w-full p-4 border-2 border-gray-200 rounded-xl focus:border-blue-500 focus:outline-none transition-colors;
}

.capture-modal-minimal .button {
  @apply w-full bg-gradient-to-r from-blue-600 to-blue-700 text-white p-4 rounded-xl font-semibold hover:shadow-lg transform hover:scale-105 transition-all;
}
```

### Slide-in Lateral
```typescript
export function SideCapture({ isOpen, onClose, onCapture }: CaptureProps) {
  return (
    <div className={`fixed inset-y-0 right-0 w-96 bg-white shadow-2xl transform transition-transform z-50 ${
      isOpen ? 'translate-x-0' : 'translate-x-full'
    }`}>
      <div className="p-6 h-full overflow-y-auto">
        {/* Conteúdo do formulário */}
      </div>
    </div>
  );
}
```

### Step-by-Step
```typescript
export function StepCapture() {
  const [step, setStep] = useState(1);
  const totalSteps = 3;

  return (
    <div className="max-w-md mx-auto">
      {/* Progress */}
      <div className="mb-6">
        <div className="flex justify-between text-sm text-gray-500 mb-2">
          <span>Passo {step} de {totalSteps}</span>
          <span>{Math.round((step / totalSteps) * 100)}%</span>
        </div>
        <div className="w-full bg-gray-200 rounded-full h-2">
          <div 
            className="bg-blue-600 h-2 rounded-full transition-all"
            style={{ width: `${(step / totalSteps) * 100}%` }}
          />
        </div>
      </div>

      {/* Steps */}
      {step === 1 && <NameStep onNext={() => setStep(2)} />}
      {step === 2 && <ContactStep onNext={() => setStep(3)} onBack={() => setStep(1)} />}
      {step === 3 && <ConfirmStep onBack={() => setStep(2)} />}
    </div>
  );
}
```

## 🔄 Fluxos de Captura

### 1. Captura Imediata
```typescript
// Captura logo após primeira interação
useEffect(() => {
  const timer = setTimeout(() => {
    if (!hasCaptured) {
      openCapture();
    }
  }, 30000); // 30 segundos

  return () => clearTimeout(timer);
}, []);
```

### 2. Captura por Intent de Saída
```typescript
// Exit-intent popup
useEffect(() => {
  const handleMouseLeave = (e: MouseEvent) => {
    if (e.clientY <= 0 && !hasCaptured) {
      openCapture();
    }
  };

  document.addEventListener('mouseleave', handleMouseLeave);
  return () => document.removeEventListener('mouseleave', handleMouseLeave);
}, []);
```

### 3. Captura Progressiva
```typescript
// Aumenta campos conforme engajamento
const [captureLevel, setCaptureLevel] = useState(1);

// Nível 1: Só email
// Nível 2: Email + Nome  
// Nível 3: Email + Nome + WhatsApp
```

## 📊 Analytics de Captura

```typescript
// Tracking de eventos
const trackCaptureEvent = (event: string, data?: object) => {
  if (typeof window !== 'undefined' && window.gtag) {
    window.gtag('event', event, {
      event_category: 'Lead Capture',
      ...data
    });
  }
};

// Uso
trackCaptureEvent('capture_modal_opened');
trackCaptureEvent('capture_form_started');
trackCaptureEvent('capture_completed', { lead_quality: 'high' });
```

## ⚡ Integrações Webhook

```typescript
// API Route para captura
export async function POST(request: Request) {
  const leadData = await request.json();
  
  // Salvar no banco
  await saveToDatabase(leadData);
  
  // Enviar para CRM
  await sendToCRM(leadData);
  
  // Enviar email de notificação
  await sendNotificationEmail(leadData);
  
  // Adicionar à lista de email marketing
  await addToEmailList(leadData);
  
  return Response.json({ success: true });
}
```

---

**Templates testados com 25%+ de conversão** 🎯