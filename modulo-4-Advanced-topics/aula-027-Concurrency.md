

## Reserved and Unreserved Concurrency

1000 (default account concurrency)




### Como funciona o **"Concurrency"** no AWS Lambda

**Concurrency** (Concorrência) no AWS Lambda refere-se ao número de instâncias da função Lambda que podem ser executadas simultaneamente para processar eventos.

---

## ✅ Conceitos Principais

### 1. **Invocation model**

* Toda vez que um evento dispara a Lambda, a AWS cria uma instância isolada da função.
* Se múltiplos eventos ocorrerem ao mesmo tempo, múltiplas instâncias podem ser criadas em paralelo.
* O número total dessas instâncias simultâneas é chamado de **concurrency**.

---

## ✅ Tipos de Concurrency

### 1. **Unreserved Concurrency (Concorrência não reservada)**

* Padrão para todas as funções.
* Compartilha a capacidade total de execução simultânea da conta.
* Se uma função consumir muitos recursos, pode impactar outras funções.

---

### 2. **Reserved Concurrency (Concorrência Reservada)**

* Você pode reservar um número fixo de instâncias simultâneas para uma função.
* Benefícios:

  * Garante que a função tenha capacidade disponível.
  * Evita que uma função consuma toda a capacidade de concorrência da conta.
  * Limita o número máximo de execuções simultâneas, atuando como um throttle.

---

### 3. **Provisioned Concurrency (Concorrência Provisionada)**

* Mantém um número definido de instâncias da função **pré-inicializadas** e prontas para executar imediatamente.
* Benefícios:

  * Elimina **cold starts** (tempo de inicialização).
  * Ideal para aplicações críticas que precisam de baixa latência.
* Custo adicional: Você paga pela quantidade de instâncias provisionadas, mesmo se não estiverem processando eventos.

---

## ✅ Como funciona na prática?

1. Um evento dispara a Lambda.
2. Se há uma instância livre, ela processa o evento.
3. Se não há instâncias livres e a função não atingiu o limite de concorrência, uma nova instância é criada.
4. Se a função atinge o limite de concorrência (reservada ou total), as invocações adicionais são:

   * Enfileiradas (no caso de invocações assíncronas).
   * Retornam erro `429 - Too Many Requests` (no caso de invocações síncronas).

---

## ✅ Limites de Concurrency

* Por padrão, cada conta tem um **limite regional** de concorrência (por ex., 1000 instâncias simultâneas).
* É possível solicitar aumento desse limite via AWS Support.
* **Reserved Concurrency** é deduzido do limite total da conta.

---

## ✅ Boas práticas

* Use **Reserved Concurrency** para funções críticas, garantindo capacidade.
* Use **Provisioned Concurrency** para reduzir cold starts em aplicações sensíveis à latência.
* Monitore métricas de concorrência via **Amazon CloudWatch** para ajustar configurações conforme necessário.

---





Perfeito! Aqui vai uma explicação clara e organizada sobre as diferenças entre **Unreserved Concurrency** e **Reserved Concurrency** no AWS Lambda, incluindo **cuidados**, **dicas** e uma **tabela comparativa**.

---

## ✅ Diferenças entre Unreserved Concurrency e Reserved Concurrency

### **Unreserved Concurrency**

* **Definição:** Capacidade de concorrência compartilhada entre todas as funções que **não possuem** concorrência reservada.
* **Comportamento:** Todas as funções competem pelo mesmo pool de concorrência disponível.
* **Impacto:** Se uma função consumir muita capacidade, pode afetar outras funções.

---

### **Reserved Concurrency**

* **Definição:** Capacidade de concorrência **dedicada exclusivamente** a uma função específica.
* **Comportamento:** Garante que a função sempre terá capacidade até o limite definido.
* **Impacto:** Evita que outras funções interfiram na disponibilidade da função reservada, mas reduz a capacidade disponível para as demais funções.

---

## ⚠️ Cuidados importantes

### Para **Unreserved Concurrency**:

* Risco de **"noisy neighbor"**: uma função pode monopolizar recursos, prejudicando outras.
* Monitorar uso de concorrência para evitar falhas por falta de capacidade.

### Para **Reserved Concurrency**:

* Reservar muita capacidade pode deixar pouca concorrência disponível para outras funções.
* Reservar pouca capacidade pode gerar throttling se a demanda superar a reserva.
* Reserved Concurrency **define também o limite máximo** de invocações simultâneas daquela função — mesmo que haja mais demanda, a função não passará desse número.

---

## 💡 Dicas práticas

1. ✅ Use **Reserved Concurrency** para funções críticas que **não podem sofrer throttling**.
2. ✅ Mantenha funções menos importantes com **Unreserved Concurrency** para flexibilizar o uso de recursos.
3. ✅ Monitore a métrica `ConcurrentExecutions` no **CloudWatch** para ajustar limites conforme necessário.
4. ✅ Antes de reservar, analise o **padrão de tráfego** da função para evitar reservas excessivas ou insuficientes.
5. ✅ Combine com **Provisioned Concurrency** para eliminar **cold starts** em funções sensíveis à latência.

---

## 📊 Tabela Comparativa: Unreserved vs Reserved Concurrency

| Característica                              | Unreserved Concurrency                    | Reserved Concurrency                        |
| ------------------------------------------- | ----------------------------------------- | ------------------------------------------- |
| **Capacidade dedicada**                     | ❌ Não                                     | ✅ Sim                                       |
| **Compartilha recursos com outras funções** | ✅ Sim                                     | ❌ Não                                       |
| **Protege contra esgotamento de recursos**  | ❌ Não                                     | ✅ Sim                                       |
| **Define limite máximo de invocações**      | ❌ Não                                     | ✅ Sim                                       |
| **Afeta concorrência de outras funções**    | ✅ Sim                                     | ✅ Sim (reduz concorrência total disponível) |
| **Ideal para**                              | Funções não críticas, workloads variáveis | Funções críticas, workloads previsíveis     |
| **Configuração**                            | Padrão, não exige configuração            | Requer definição explícita de reserva       |

---








- Enviando pedido de aumento de quota na AWS
tava em 10 o valor de "Concurrent executions"
Submitting Quota increase request for Concurrent executions with requested Value of 1223.