---
title: "Jak získat odpovědi o Funcionário Infinito"
description: Použijte LLM k rychlému zodpovězení vašich otázek o Funcionário Infinito
sidebar:
  order: 3
---

## Začněte zde: Funcionário Infinito-Help

**Nejrychlejší způsob, jak získat odpovědi o Funcionário Infinito, je skill `funcionario-help`.** Tento inteligentní průvodce zodpoví více než 80 % všech otázek a je vám k dispozici přímo ve vašem IDE při práci.

Funcionário Infinito-Help je víc než vyhledávací nástroj — umí:
- **Prozkoumat váš projekt** a zjistit, co už bylo dokončeno
- **Rozumět přirozenému jazyku** — ptejte se běžnou řečí
- **Přizpůsobit se nainstalovaným modulům** — zobrazí relevantní možnosti
- **Automaticky se spouštět po workflow** — řekne vám přesně, co dělat dál
- **Doporučit první povinný úkol** — žádné hádání, kde začít

### Jak používat Funcionário Infinito-Help

Zavolejte ho jménem ve vaší AI relaci:

```
funcionario-help
```

:::tip
V závislosti na vaší platformě můžete také použít `/funcionario-help` nebo `$funcionario-help`, ale samotné `funcionario-help` by mělo fungovat všude.
:::

Spojte ho s dotazem v přirozeném jazyce:

```
funcionario-help I have a SaaS idea and know all the features. Where do I start?
funcionario-help What are my options for UX design?
funcionario-help I'm stuck on the PRD workflow
funcionario-help Show me what's been done so far
```

Funcionário Infinito-Help odpoví:
- Co je doporučeno pro vaši situaci
- Jaký je první povinný úkol
- Jak vypadá zbytek procesu

## Kdy použít tohoto průvodce

Použijte tuto sekci, když:
- Chcete pochopit architekturu nebo interní fungování Funcionário Infinito
- Potřebujete odpovědi mimo to, co Funcionário Infinito-Help nabízí
- Zkoumáte Funcionário Infinito před instalací
- Chcete prozkoumat zdrojový kód přímo

## Kroky

### 1. Vyberte si zdroj

| Zdroj                | Nejlepší pro                              | Příklady                     |
| -------------------- | ----------------------------------------- | ---------------------------- |
| **Složka `_funcionario`**   | Jak Funcionário Infinito funguje — agenti, workflow, prompty | „Co dělá PM agent?“        |
| **Celý GitHub repo** | Historie, instalátor, architektura        | „Co se změnilo ve v6?“      |

Složka `_funcionario` se vytvoří při instalaci Funcionário Infinito. Pokud ji ještě nemáte, naklonujte si repo.

### 2. Nasměrujte AI na zdroj

**Pokud vaše AI umí číst soubory (Claude Code, Cursor atd.):**

- **Funcionário Infinito nainstalován:** Nasměrujte na složku `_funcionario` a ptejte se přímo
- **Chcete hlubší kontext:** Naklonujte si [celé repo](https://github.com/testemileum/funcionario-infinito)

**Pokud používáte ChatGPT nebo Claude.ai:**

Otevřete [dokumentaci Funcionário Infinito](https://docs.funcionario-infinito.com.br/).

### 3. Položte svou otázku

:::note[Příklad]
**O:** „Řekni mi nejrychlejší způsob, jak něco vytvořit s Funcionário Infinito“

**A:** Spusťte `funcionario-build`. Předejte přímý záměr, issue, specifikaci nebo naplánovanou story; workflow využije dostupný kontext a zvolí potřebnou hloubku upřesnění, plánování, implementace a revize.
:::

## Co získáte

Přímé odpovědi o Funcionário Infinito — jak agenti fungují, co dělají workflow, proč jsou věci strukturované tak, jak jsou — bez čekání na odpověď od někoho jiného.

## Tipy

- **Ověřte překvapivé odpovědi** — LLM se občas mýlí. Zkontrolujte zdrojový soubor nebo se zeptejte na Discordu.
- **Buďte konkrétní** — „Co dělá krok 3 PRD workflow?“ je lepší než „Jak funguje PRD?“

## Stále jste uvízli?

Zkusili jste přístup přes LLM a stále potřebujete pomoc? Nyní máte mnohem lepší otázku k položení.

| Kanál                     | Použijte pro                                |
| ------------------------- | ------------------------------------------- |
| `#funcionario-method-help`       | Rychlé otázky (chat v reálném čase)         |
| `help-requests` fórum     | Detailní otázky (vyhledatelné, trvalé)      |
| `#suggestions-feedback`   | Nápady a požadavky na funkce                |
| `#report-bugs-and-issues` | Hlášení chyb                                |

**Discord:** [discord.gg/SEU-CONVITE-AQUI](https://discord.gg/SEU-CONVITE-AQUI)

**GitHub Issues:** [github.com/testemileum/funcionario-infinito/issues](https://github.com/testemileum/funcionario-infinito/issues) (pro jasné chyby)
