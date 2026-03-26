---
layout: post
title: "Como baixei a temperatura do meu Dell de 100°C para 70°C"
date: 2026-03-25
categories: hardware suporte
image: /assets/images/dell-temp-hero.png
featured-color: "#ff006e"
excerpt: "Descubra como remover antivírus pesados e otimizar processos de fundo pode salvar seu notebook. Meu Dell caiu de 100°C para 70°C!"
---

Neste post, documento como a remoção de um antivírus pesado e o ajuste de processos de fundo salvaram a vida útil do meu i5 de 13ª geração.

## 🔥 O Problema

Meu Dell estava rodando constantemente a 100°C. Qualquer tarefa pesada (compilação, renders) era impossível. O notebook desligava sozinho por proteção térmica.

## 🛡️ Culpado: O Antivírus Pesado

O principal vilão era um antivírus corporativo que:
- Varria a memória e disco constantemente
- Usava 30-40% de CPU em idle
- Consumia 2-3GB de RAM

## ✅ Soluções Aplicadas

### 1. Removimento do Antivírus Pesado
```powershell
# Desinstalei via Control Panel e realizei limpeza de registro
Reg Clean realizado com CCleaner
```

### 2. Ajuste de Processos de Fundo
- Desabilitei Windows Search indexação
- Removi telemetria desnecessária
- Desabilitei superfetch e prefetch
- Removi inicializações desnecessárias via msconfig

### 3. Limitador de CPU
- Instalei NotebookFanControl para melhor ventilação
- Ajustei plano de energia para "Alto Desempenho"
- Limpeza física das entradas de ar

## 📊 Resultados

| Métrica | Antes | Depois | Melhora |
|---------|-------|--------|--------|
| Temperatura Idle | ~85°C | ~45°C | **-47%** |
| Temperatura Carga | 100°C | 70°C | **-30°C** |
| CPU em Idle | 35% | 8% | **-27%** |
| RAM em Uso | 5.2GB | 2.8GB | **-2.4GB** |

## 💡 Lições Aprendidas

1. Antivírus corporativos podem ser piores que os vírus
2. Telemetria é um assassino silencioso de performance
3. Limpeza física importa tanto quanto a virtual
4. Windows pode ser muito mais ágil sem bloatware

---

**Moral da história:** Às vezes, menos é mais. Remover detritos é mais eficiente que adicionar otimizadores.