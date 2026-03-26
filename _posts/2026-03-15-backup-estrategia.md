---
layout: post
title: "Estratégia de Backup 3-2-1: Nunca Perca seus Dados"
date: 2026-03-15
categories: backup segurança
excerpt: "A estratégia de backup 3-2-1 é o padrão da indústria. Aprenda como implementá-la e durmir tranquilo."
featured-color: "#39ff14"
---

Perdi 500GB de dados em 2019 por falta de backup. Desde então, sigo uma regra religiosamente: **3-2-1**.

## 💔 Por Que Não é "Quando", é "Se"

Seus dados podem ser perdidos por:
- 🔥 Falha de HD/SSD
- ⚡ Surto elétrico
- 🦠 Ransomware/Malware
- 🌊 Desastre natural
- 🤦 Deletar acidentalmente

## 📋 A Regra 3-2-1

```
3 cópias do seu dado
2 mídias diferentes
1 cópia fora do site
```

### Exemplo Prático

```
Dados Originais: Meu Notebook
├── Cópia 1: HD Externo (LOCAL)
├── Cópia 2: Pendrive (LOCAL)
└── Cópia 3: Google Drive / OneDrive (NUVEM)
```

## 🔧 Implementação Passo a Passo

### Passo 1: Identifique o Que Fazer Backup

```
CRÍTICO (Backup semanal):
- Documentos de trabalho
- Fotos pessoais
- Projetos de código
- Configurações importantes

IMPORTANTE (Backup mensal):
- Educação/Cursos
- Arquivos de referência
- Downloads organizados

NÃO CRÍTICO (Backup anual):
- Programas instáveis
- Torrents
- Arquivos temporários
```

### Passo 2: Escolha as Ferramentas

#### Para Windows
```powershell
# Opção 1: Windows Backup (Nativo)
wbadmin start backup -backupTarget:D: -include:C: -allCritical

# Opção 2: Macrium Reflect (Profissional)
# https://www.macrium.com/reflectfree

# Opção 3: Veeam (Enterprise)
# https://www.veeam.com/
```

#### Para Linux
```bash
# rsync (o ouro puro)
rsync -av --delete /home/user/ /mnt/backup/

# Alternatively: Timeshift (GUI)
sudo timeshift --create
```

### Passo 3: Configure Schedule Automático

#### Windows PowerShell Script
```powershell
# Salvar como: C:\Scripts\backup.ps1
$source = "C:\Users\Nickolas\Documents"
$dest1 = "E:\Backup" # HD Externo
$dest2 = "F:\BackupUSB" # Pendrive

# Executar robocopy
robocopy $source $dest1 /MIR /Z /R:3
robocopy $source $dest2 /MIR /Z /R:3

# Log
Add-Content -Path "C:\logs\backup.log" -Value "Backup executado: $(Get-Date)"
```

#### Agendar via Task Scheduler
```
Frequência: Semanal (Domingo 2:00 AM)
Ação: C:\Scripts\backup.ps1
```

### Passo 4: Nuvem (A Cópia Remota)

Escolha um serviço:

| Serviço | Preço | Características |
|---------|-------|-----------------|
| **Google Drive** | R$ 20/mês | 100GB, integrado |
| **OneDrive** | R$ 20/mês | 100GB, Microsoft |
| **BackBlaze** | R$ 65/ano | **Backup ilimitado** ⭐ |
| **Sync.com** | R$ 8/mês | Privado, criptografado |

**Recomendação:** Para dados críticos, use BackBlaze (backup automático completo).

```powershell
# Instalar BackBlaze
choco install backblaze

# Ou download manual: https://www.backblaze.com
```

## 🧪 O Teste Crucual: Restore

Fazer backup é inútil se você não conseguir restaurar!

### Teste Mensal
1. Selecione um arquivo crítico
2. Delete-o completamente
3. Restaure a partir do backup
4. Documente o tempo e sucesso

```powershell
# Exemplo de teste
$file = "C:\Users\Nickolas\Documents\Palestra_Importante.pptx"
Remove-Item $file -Force
# Aguarde 5 minutos...
# Restaure do backup
Copy-Item E:\Backup\Palestra_Importante.pptx $file
```

## 💡 Dicas Profissionais

### 1. Versioning
Configure backups incrementais para manter histórico:
```
Backup_2026-03-15
Backup_2026-03-22
Backup_2026-03-29
```

### 2. Encryption
Sempre criptografe backups remotos:
```bash
# Linux
gpg --encrypt backup_file.tar.gz

# Windows
cipher /e /s:C:\Backups
```

### 3. Verificação de Integridade
```powershell
# SHA256 hash para verificar corrupção
certutil -hashfile backup.zip SHA256 | Tee-Object -FilePath backup.hash

# Verificar depois
certutil -hashfile backup.zip SHA256 | findstr /V "SHA256"
```

## 📊 Meu Setup Pessoal

```
Backup Diário:
├── Windows File History (C:\ para HD Externo)
├── Veeam Agent (Imagem do Sistema para Nuvem)
└── Sync.com (Sincronização em tempo real)

Backup Semanal:
└── BackBlaze (Backup completo automático)

Teste de Restore:
└── 1º domingo do mês
```

## 🎯 Checklist

- ☐ Identifiquei dados críticos
- ☐ Escolhi ferramenta de backup
- ☐ Criei cópias locais (pelo menos 2)
- ☐ Configurei backup em nuvem
- ☐ Agendei backup automático
- ☐ Realizei teste de restore
- ☐ Documentei a estratégia

---

**Lembrança:** Seu backup não é tão bom quanto seu teste de restore. Não ignore esse passo!
