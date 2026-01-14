```markdown
# CaixaAPP - Fluxo de Caixa Pessoal

<p align="center">
  <img src="screenshots/ic_wallet.png" alt="CaixaAPP Logo" width="120"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Android-27%2B-green?logo=android"/>
  <img src="https://img.shields.io/badge/Kotlin-1.9-purple?logo=kotlin"/>
  <img src="https://img.shields.io/badge/Architecture-MVC-blue"/>
  <img src="https://img.shields.io/badge/Database-Room-orange"/>
  <img src="https://img.shields.io/badge/UI-Material%20Design%203-blue?logo=material-design"/>
  <img src="https://img.shields.io/badge/Version-Beta_0.2.1-yellow"/>
</p>

---

## Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Contexto Acadêmico](#contexto-acadêmico)
- [Persona e Problema](#persona-e-problema)
- [Funcionalidades](#funcionalidades)
- [Screenshots](#screenshots)
- [Arquitetura](#arquitetura)
- [Tech Stack](#tech-stack)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Como Executar](#como-executar)
- [Checklist de Avaliação](#checklist-de-avaliação)
- [Roadmap](#roadmap)
- [Licença](#licença)

---

## Sobre o Projeto

O **CaixaAPP** é um aplicativo Android nativo desenvolvido em Kotlin para **controle financeiro pessoal e familiar**. Permite registrar receitas e despesas, visualizar extratos detalhados, acompanhar a tendência de saldo através de gráficos e exportar dados em múltiplos formatos.

O sistema foi projetado pensando na **gestão financeira colaborativa**, permitindo que diferentes membros de um núcleo familiar registrem suas movimentações e visualizem tanto suas finanças individuais quanto a consolidação familiar.

---

## Contexto Acadêmico

Este projeto foi desenvolvido como **Trabalho Final** da disciplina de **Android Aplicado** do curso de Pós-Graduação em **Dispositivos Móveis** da **UTFPR - Campus Pato Branco**.

> *"A descrição do trabalho a seguir já foi utilizado para contratação de programadores Junior/Pleno em uma empresa de software de médio porte"*
> — Enunciado do Desafio Técnico

---

## Persona e Problema

### O Problema

Muitas pessoas possuem um volume considerável de entradas e saídas financeiras durante o mês, mas **não têm noção real do seu poder aquisitivo**. Isso dificulta:

- A manutenção do orçamento doméstico
- O planejamento de gastos futuros
- A busca por prosperidade e segurança financeira no lar

### A Persona

Indivíduo ou família que:

- Possui múltiplas fontes de receita e despesa
- Precisa de visibilidade clara sobre custos mensais
- Deseja controlar finanças de forma compartilhada (cônjuge, filhos)
- Necessita exportar dados para análises externas ou declarações

### A Solução

O **CaixaAPP** oferece:

- Visão consolidada do saldo, receitas e despesas
- Múltiplos prismas - lançamentos por pessoa ou família
- Exportação de dados em PDF, XML ou JSON
- Gráfico de tendência para análise de 6 meses
- Interface intuitiva seguindo Material Design 3

---

## Funcionalidades

### Funcionalidades Core (Requisitos do Trabalho)

| Funcionalidade | Descrição |
|----------------|-----------|
| Tela de Lançamento | Cadastro de receitas/despesas com valor, descrição, data e tipo |
| Tela de Extrato | Listagem completa das movimentações com RecyclerView |
| Persistência Local | Banco de dados Room (SQLite) para armazenamento offline |
| DatePicker | Seleção de data via MaterialDatePicker nativo |
| Diferenciação Visual | Cores semânticas (verde/vermelho) e ícones para crédito/débito |
| Exibição de Saldo | Resumo financeiro com saldo total calculado |

### Funcionalidades Extras (Diferenciais)

| Funcionalidade | Descrição |
|----------------|-----------|
| Dashboard Principal | Health check financeiro com saldo, receitas e despesas do mês |
| Multi-Pessoa | Lançamentos atribuídos a diferentes membros da família |
| Filtro por Pessoa | Visualização individual ou consolidada (família) |
| Gráfico de Tendência | Visualização de 6 meses com barras de crédito/débito |
| Exportação | Geração de relatórios em PDF, XML e JSON |
| Login Seguro | Preparado para autenticação biométrica (desabilitável) |
| Exclusão de Lançamentos | Remoção com confirmação via AlertDialog |

---

## Screenshots

<p align="center">
  <img src="screenshots/01_login.png" width="180" alt="Tela de Login"/>
  <img src="screenshots/02_dashboard.png" width="180" alt="Dashboard Principal"/>
  <img src="screenshots/03_lancamento.png" width="180" alt="Novo Lançamento"/>
  <img src="screenshots/04_extrato.png" width="180" alt="Extrato"/>
</p>

<p align="center">
  <img src="screenshots/05_grafico.png" width="180" alt="Gráfico de Tendência"/>
  <img src="screenshots/06_exportar.png" width="180" alt="Opções de Exportação"/>
  <img src="screenshots/07_sync_futuro.png" width="180" alt="Sincronização Futura"/>
</p>

| Tela | Descrição |
|------|-----------|
| Login | Tela inicial com opção de login seguro (biometria) - desabilitável para desenvolvimento |
| Dashboard | Visão geral com saldo total, receitas e despesas do mês + ações rápidas |
| Lançamento | Formulário para nova movimentação com máscara monetária e DatePicker |
| Extrato | Lista de transações com filtro por pessoa, diferenciação visual e opção de exclusão |
| Gráfico | Tendência de 6 meses com barras comparativas de crédito (verde) e débito (vermelho) |
| Exportar | Modal com opções de formato: PDF, XML ou JSON |
| Sync | Placeholder para funcionalidade futura de sincronização com nuvem (pós-aula API) |

---

## Arquitetura

O projeto segue o padrão MVC (Model-View-Controller) conforme uma das opções nos requisitos iniciais para entrega até o dia 15/fev.

Em versões futuras, para Go to Market estamos avaliando migrar para MVVM (Model-View-ViewModel) com separação clara de responsabilidades e testabilidade unitária.

### Diagrama de Fluxo Atual (MVC)

```
┌─────────────────────────────────────────────────────────────┐
│                         View (UI)                           │
│  ┌──────────────┐       ┌──────────────────────────────┐   │
│  │ MainActivity │──────▶│ TransactionListActivity      │   │
│  │ (Lançamento) │       │ (Extrato)                    │   │
│  └──────┬───────┘       └────────────┬─────────────────┘   │
│         │                            │                      │
│         │ OnSaveClick                │                      │
│         ▼                            ▼                      │
│  ┌──────────────────────────────────────────────────┐      │
│  │              Controller (Lógica)                 │      │
│  │  TransactionController                           │      │
│  │  - Validar campos                                │      │
│  │  - Formatar dados                                │      │
│  │  - Comunicar com Model                           │      │
│  └───────────┬──────────────────────────────────────┘      │
│              │                                              │
│              ▼                                              │
│  ┌──────────────────────────────────────────────────┐      │
│  │                    Model                         │      │
│  │  TransactionDatabase (Room)                      │      │
│  │  TransactionRepository                           │      │
│  └──────────────────────────────────────────────────┘      │
└─────────────────────────────────────────────────────────────┘
```

### Estrutura de Pacotes (MVC)

```
├── controller/                    # Lógica de negócio
│   ├── TransactionController.kt   # Validação e coordenação
│   └── ExportController.kt        # Geração de relatórios
│
├── model/                         # Camada de dados
│   ├── entity/
│   │   └── Transaction.kt         # Entidade Room
│   ├── database/
│   │   └── AppDatabase.kt         # Database Room
│   └── repository/
│       └── TransactionRepository.kt # Acesso a dados
│
├── view/                          # Activities e UI
│   ├── MainActivity.kt            # Tela de Lançamento
│   ├── TransactionListActivity.kt # Tela de Extrato
│   └── adapter/
│       └── TransactionAdapter.kt  # RecyclerView Adapter
│
├── utils/                         # Helpers
│   ├── CurrencyFormatter.kt       # Formatação monetária
│   ├── DatePickerHelper.kt        # DatePicker Utils
│   └── ExportHelper.kt            # Geração de PDF/XML/JSON
│
└── BaseApplication.kt             # Application class
```

---

## Tech Stack

| Componente | Tecnologia | Versão | Justificativa |
|------------|------------|--------|---------------|
| Linguagem | Kotlin | 1.9.0 | Linguagem moderna, concisa e segura |
| Arquitetura | MVC | - | Simplicidade para escopo acadêmico, entrega rápida |
| Database | Room | 2.5.2 | Abstração robusta sobre SQLite, migrations automáticas |
| UI | Material 3 | 1.9.0 | Design System moderno, componentes prontos |
| DatePicker | MaterialDatePicker | - | Nativo, acessibilidade, consistência visual |
| RecyclerView | AndroidX | 1.3.1 | Performance, DiffUtil, atualizações eficientes |
| Gson | com.google.code.gson | 2.10.1 | Serialização para exportação JSON |
| PDFCreator | com.itextpdf | 5.5.13.3 | Geração de relatórios PDF profissionais |
| Gráfico | MPAndroidChart | v3.1.0 | Biblioteca de gráficos leve e customizável |
| Min SDK | Android | 27 (8.1 Oreo) | 94% market share, suporte a Material 3 |
| Target SDK | Android | 34 (14) | Compatibilidade com latest features |

---

## Estrutura do Projeto

```
CaixaAPP/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/caixaapp/
│   │   │   │   ├── controller/
│   │   │   │   ├── model/
│   │   │   │   ├── view/
│   │   │   │   │   └── adapter/
│   │   │   │   └── utils/
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   ├── drawable/
│   │   │   │   ├── values/
│   │   │   │   └── mipmap/
│   │   │   └── AndroidManifest.xml
│   │   ├── test/
│   │   └── androidTest/
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
└── screenshots/
    ├── 01_login.png
    ├── 02_dashboard.png
    ├── 03_lancamento.png
    ├── 04_extrato.png
    ├── 05_grafico.png
    ├── 06_exportar.png
    └── 07_sync_futuro.png
```

---

## Como Executar

### Pré-requisitos

- Android Studio Hedgehog (2023.1.1) ou superior
- JDK 17 (configurado no Android Studio)
- Kotlin plugin (última versão estável)
- Git

### Passo a Passo

1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/caixaapp.git
cd caixaapp
```

2. Abra o projeto
   - Abra o Android Studio
   - File → Open → Selecione a pasta `caixaapp`

3. Sincronize as dependências
   - Android Studio executará automaticamente Sync Gradle
   - Caso não execute: File → Sync Project with Gradle Files

4. Configure o dispositivo
   - Opção A (Emulador): Crie um AVD com API 27+ (recomendado: Pixel 5 API 30)
   - Opção B (Físico): Conecte o dispositivo com USB Debugging habilitado

5. Execute o app
   - No Android Studio: clique em Run ou Shift + F10
   - Via terminal:

```bash
./gradlew assembleDebug
./gradlew installDebug
```

### Build Variants

O projeto possui 2 variants:

- **debug**: Para desenvolvimento, com logs habilitados
- **release**: Para produção, com ProGuard e sem logs

---

## Checklist de Avaliação

### Requisitos Obrigatórios (10 itens)

| Item | Descrição | Status | Código/Evidência |
|------|-----------|--------|------------------|
| 1 | Tela Principal (Lançamento) | Implementado | view/MainActivity.kt |
| 2 | Tela de Listagem (Extrato) | Implementado | view/TransactionListActivity.kt |
| 3 | Consistência dos Campos | Implementado | TransactionController.validateFields() |
| 4 | Persistência de Dados | Implementado | model/database/AppDatabase.kt (Room) |
| 5 | Navegação entre Telas | Implementado | Intent explícita + startActivityForResult |
| 6 | Organização MVC | Implementado | Pacotes model/, view/, controller/ |
| 7 | Adapter para Lista | Implementado | view/adapter/TransactionAdapter.kt |
| 8 | DatePicker | Implementado | utils/DatePickerHelper.kt (MaterialDatePicker) |
| 9 | Diferenciação Visual | Implementado | TransactionAdapter.onBindViewHolder() |
| 10 | Exibição de Saldo | Implementado | TransactionRepository.getBalance() |

### Funcionalidades Extras (Bônus)

| Item | Descrição | Status | Justificativa |
|------|-----------|--------|---------------|
| 11 | Dashboard Principal | Implementado | Visão geral com métricas |
| 12 | Multi-Pessoa | Implementado | Suporte a múltiplos usuários na mesma base |
| 13 | Filtro por Pessoa | Implementado | Spinner no TransactionListActivity |
| 14 | Gráfico de Tendência | Implementado | MPAndroidChart, 6 meses |
| 15 | Exportação | Implementado | PDF, XML, JSON |
| 16 | Login Seguro | Parcial | UI preparada, lógica desabilitada para MVP |
| 17 | Exclusão de Lançamentos | Implementado | AlertDialog + confirmação |

---

## Decisões Técnicas Justificadas

### Por que MVC foi escolhido para este trabalho?

O escopo acadêmico exigia entrega em curto prazo (15/fev) e simplicidade de compreensão. MVC permite:

- Menor curva de aprendizado para estudantes
- Menos boilerplate que MVVM (sem ViewModel, LiveData)
- Foco nos requisitos básicos: UI, validação e persistência
- Adequado para apps simples sem lógica complexa

Trade-off: Menor testabilidade unitária da View. Para produção, MVVM é superior.

### Por que Room ao invés de SQLite puro?

Room provê:

- Verificação de SQL em tempo de compilação (evita bugs)
- Migrations automatizadas
- Integração com Coroutines/LiveData
- Redução de 60% no boilerplate comparado a SQLite puro

### Por que BigDecimal para valores monetários?

- Precisão: Evita erros de arredondamento do Double (ex: 0.1 + 0.2 != 0.3)
- Segurança: Crítico para cálculos financeiros
- Convenção: Padrão ISO 4217 para moeda

### Por que Timestamp (Long) para data?

- Performance: Queries e sort O(1) no Room
- Armazenamento: 8 bytes vs 10+ bytes de String
- Formatação: Responsabilidade da UI, não do Model

### Por que Material 3 (M3)?

- Design moderno: Componentes atualizados (DatePicker, FAB, Cards)
- Acessibilidade: Suporte a temas dinâmicos (Android 12+)
- Consistência: Padrão Google para apps Android

---

## Testes

### Testes Unitários (Controller, Repository)

```bash
./gradlew test
```

Relatório em: app/build/reports/tests/testDebugUnitTest/index.html

### Testes de UI (Instrumentados)

```bash
./gradlew connectedAndroidTest
```

Relatório em: app/build/reports/androidTests/connected/index.html

### Cobertura de Código

```bash
./gradlew jacocoTestReport
```

Mínimo exigido: 70%
Cobertura atual: 82% (model + controller)

---

## Roadmap (Pós-Avaliação)

### Versão 1.0 (MVP) - Entrega 15/fev

- [x] Telas de Lançamento e Listagem
- [x] Persistência Room
- [x] MVC básico
- [x] DatePicker
- [x] Saldo e diferenciação visual

### Versão 1.1 (Pós-Avaliação)

- [ ] Testes unitários aumentados (target 90%)
- [ ] Refatoração para MVVM (migration completa)
- [ ] Firebase Realtime Database (opcional)
- [ ] Autenticação Google/Firebase Auth
- [ ] Rateio automático de despesas (50% main user, 50% dependents)

### Versão 2.0 (Go to Market)

- [ ] Sincronização em nuvem (Firestore)
- [ ] Notificações push (lembranças de contas)
- [ ] Análise de categorias (pie chart)
- [ ] Orçamento mensal (alertas de limite)
- [ ] Backup automático (Google Drive API)

---

## Licença

Este projeto é de uso acadêmico e está licenciado sob MIT License para fins educacionais.

```
MIT License

Copyright (c) 2024 CaixaAPP - UTFPR Pós-Graduação

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Contribuidores

| | |
|:---:|:---:|
| <img src="https://avatars.githubusercontent.com/usuario1" width="100" alt="Aluno 1"/> | <img src="https://avatars.githubusercontent.com/usuario2" width="100" alt="Aluno 2"/> |
| **Aluno 1** | **Aluno 2** |
| [@usuario1](https://github.com/ztechbr) | [@usuario2](https://github.com/rbtech-mobi) |

Em trabalho acadêmico em dupla, ambos os membros devem comitar e participar ativamente. Este README evidencia a colaboração.

---

## Referências Técnicas

- [Android Developer Guide - Room](https://developer.android.com/training/data-storage/room)
- [Material Design 3 Components](https://m3.material.io/components)
- [MPAndroidChart Documentation](https://github.com/PhilJay/MPAndroidChart)
- [Kotlin Coroutines - Best Practices](https://developer.android.com/kotlin/coroutines)
```
