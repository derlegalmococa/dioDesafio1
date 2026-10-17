# simulador-fundos-imobiliarios

Ferramenta em Excel que simula investimentos em fundos imobiliários (FIIs): do aporte mensal aos dividendos que ele rende.

## Perguntas que a ferramenta responde (aba `Simulador`)
| Pergunta | Onde aparece |
|---|---|
| 1) Quanto investir por mês? | `C14` (entrada) |
| 2) Por quantos anos? | `C15` (entrada) |
| 3) Qual a taxa de rendimento mensal? | `C16` (entrada) |
| 4) Quanto de patrimônio vai acumular? | `C17` |
| 5) Quanto vai receber de dividendos por mês? | `C18` |

A coluna **D** repete a simulação usando a **sugestão de 30% do salário** como aporte.

## Como o VF e o PROCV entram
- **VF (FV):** `=-FV(taxa_mensal; qtde_anos*12; aporte)` – taxa por período, nº de períodos (anos × 12) e pagamento por período. O sinal negativo converte o resultado em valor positivo. Dividendos = `patrimonio * rendimento_carteira`.
- **Cenários (2, 5, 10, 20, 30 anos):** mesma fórmula com referências absolutas (`$C$16`, `$C$14`) e o prazo em `$B24`.
- **PROCV (VLOOKUP) com chave composta:** na aba `Apoio`, a coluna A monta `Perfil&"-"&Tipo` (ex.: `Moderado-PAPEL`). No simulador: `=PROCV(perfil&"-"&B35; tabela_perfis; 4; FALSO)`.

## Intervalos nomeados
`salario`, `rendimento_carteira`, `pct_sugestao`, `sugestao_aporte`, `aporte`, `qtde_anos`, `taxa_mensal`, `patrimonio`, `dividendos_mensais`, `perfil`, `tabela_perfis`.

## Percentuais por perfil (exemplos didáticos, não são recomendação)
| Tipo | Conservador | Moderado | Agressivo |
|---|---|---|---|
| PAPEL | 30% | 30% | 50% |
| TIJOLO | 50% | 40% | 10% |
| HÍBRIDOS | 10% | 8% | 5% |
| FOFs | 10% | 10% | 5% |
| DESENVOLVIMENTO | 0% | 6% | 20% |
| HOTELARIA | 0% | 6% | 10% |

Origem: partem da planilha de referência do desafio. No perfil Moderado da referência a soma era 110% (32/40/8/10/10/10); ajustei DESENVOLVIMENTO e HOTELARIA para 6% e PAPEL para 30% para somar 100%. A aba `Apoio` confere a soma de cada perfil.

## O que mudei em relação à ferramenta de referência
- Banner, grade oculta, células calculadas em cinza e entradas em amarelo/azul.
- Segunda simulação com a sugestão de 30% do salário (e cenários correspondentes).
- Gráfico de pizza que muda com o perfil.
- Validação de dados nas entradas, conferência "soma 100%" e total aportado/ganho com rendimento.
- Correção do perfil Moderado (somava 110%).

Salário e valores são exemplos.
