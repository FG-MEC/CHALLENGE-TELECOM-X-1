# 📉 Churn de Clientes — Telecom X

Proyecto de análisis de datos para entender **por qué los clientes cancelan (churn)** y qué variables están más asociadas a la evasión.

---

## 🎯 Objetivo
Analizar el comportamiento de los clientes de **Telecom X** e identificar **factores clave** relacionados con el churn, para proponer **acciones de retención**.

---

## 🧰 Tecnologías
- **Python**
- **pandas**
- **numpy**
- **matplotlib**

---

## 📦 Dataset
Datos de clientes en formato **JSON** (estructura anidada). Incluye:
- Información demográfica (género, adulto mayor, etc.)
- Servicios (teléfono e internet)
- Contrato, método de pago
- Cargos mensuales y totales

---

## 🧼 Limpieza y tratamiento de datos
Se realizó un flujo simple de preparación:

- **Carga desde URL** y aplanado con `pandas.json_normalize()`
- **Estandarización de textos**: `strip()` + `lower()` para evitar inconsistencias
- **Conversión de Churn**: `"Yes"/"No"` → `1/0`
- **Total charges**: `account.Charges.Total` venía como `object` por vacíos → conversión a numérico
- **Imputación preventiva**:
  - numéricas → mediana
  - categóricas → `"unknown"`
- **Duplicados**: no se encontraron
- **Nueva variable**:
  - `Cuentas_Diarias = account.Charges.Monthly / 30`

✅ Dataset final: **7267 filas**, **22 columnas**, listo para análisis.

---

## 🔎 Análisis Exploratorio (EDA)

### 1) Distribución de Churn
- **No churn (0):** ~73.5%  
- **Churn (1):** ~26.5%

---

### 2) Variables más relevantes
**Numéricas (por correlación con churn):**
- `antiguedad_meses (tenure)`
- `cargo_mensual`
- `cargo_total`

**Categóricas (por variación de churn entre categorías):**
- `account.Contract`
- `internet.InternetService`
- `account.PaymentMethod`
- Servicios extra de internet: `OnlineSecurity`, `TechSupport`, `OnlineBackup`, `DeviceProtection`, etc.

---

### 3) Categóricas clave

**Género**
- Diferencias mínimas (no es un factor relevante).

**Tipo de contrato (factor más fuerte)**
- Mes a mes: **~41.3% churn**
- 1 año: **~10.9% churn**
- 2 años: **~2.8% churn**

**Método de pago**
- Cheque electrónico: **~43.8% churn**
- Otros métodos: ~14.8%–18.5%

---

### 4) Numéricas clave

**Antigüedad (meses)**
- Sin churn: media ~37.3, mediana ~37
- Con churn: media ~17.9, mediana ~10  
➡️ Mayor riesgo en los **primeros meses**.

**Cargo total**
- Sin churn: media ~2540, mediana ~1669
- Con churn: media ~1531, mediana ~703  
➡️ Relacionado con menor permanencia.

---

## 💡 Conclusiones e insights
1. **El contrato define el churn**: a mayor duración, menor evasión.  
   👉 Incentivar migración de *mes a mes* a planes anuales.

2. **Antigüedad crítica**: churn se concentra al inicio.  
   👉 Mejorar onboarding y seguimiento en los primeros 3–12 meses.

3. **Pago con cheque electrónico es un foco rojo**.  
   👉 Revisar perfil/experiencia de pago y promover métodos alternativos.

4. **Servicios extra de internet se asocian a fidelidad**.  
   👉 Bundles/beneficios para aumentar adopción de servicios.

5. **Género no influye** de forma relevante.  
   👉 Estrategias de retención pueden ser transversales.

---

## ▶️ Cómo ejecutar
1. Clona el repo:
   ```bash
   git clone https://github.com/FG-MEC/CHALLENGE-TELECOM-X-1.git
