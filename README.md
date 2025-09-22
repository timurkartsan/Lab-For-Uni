# Lab For Uni - Setup Instructions

### 1. Install Docker Desktop
- Go to: https://www.docker.com/products/docker-desktop/
- Download Docker Desktop for Windows
- Install with administrator privileges
- Restart your computer if prompted
- Start Docker Desktop

### 2. After Docker is Installed
Once Docker is running, I'll help you with:
- Building the Jupyter notebook Docker container
- Starting the container
- Running the code
- Committing results to your GitHub repository

### 3. GitHub Repository
You'll also need to manually create the GitHub repository:
- Go to https://github.com/timurkartsan
- Create a new repository named: "Lab For Uni"
- Make it public
- Don't initialize with README (we already have files)

## Repository Structure
```
Lab For Uni/
├── README.md (this file)
├── iad-practice/ (cloned repository)
│   ├── dev-env/ (Docker setup)
│   │   ├── docker-compose.yml
│   │   ├── Dockerfile
│   │   └── Makefile
│   └── practice/ (Jupyter notebooks)
└── .git/ (your Lab For Uni repository)
```

## Next Steps After Docker Installation
Run these commands in PowerShell from the "Lab For Uni" folder:

```bash
cd iad-practice/dev-env
docker compose build
docker compose up -d
```

Then access Jupyter at: http://localhost:8888

---

## Звіт про виконання (Report)

Нижче — контрольний список завдання та статус на момент останнього запуску:

- [x] встановити git
- [x] створити git account (GitHub: timurkartsan)
- [x] склонувати репозиторій https://github.com/djnzx/iad-practice
- [x] встановити docker (Docker Desktop)
- [x] зібрати контейнер jupiter notebook (docker compose build)
- [x] запустити jupiter notebook (docker compose up -d, порт 8888)
- [x] запустити код (автоматичне виконання всіх *.ipynb через jupyter nbconvert)

Дата/час останнього запуску: UTC 2025-09-22

### Де шукати результати

- Усі згенеровані/оновлені ноутбуки скопійовано до каталогу: results/
- Вихідні ноутбуки залишаються в iad-practice/practice/ (ці теж виконано in-place всередині контейнера)

### Як повторити виконання коду

1) Запустіть середовище:

```powershell
# з кореня репозиторію
docker compose -f "iad-practice/dev-env/docker-compose.yml" up -d --build
```

2) За бажання — повторно виконати всі ноутбуки без відкриття браузера:

```powershell
# Шукає всі *.ipynb під iad-practice\practice і запускає їх у контейнері
$root = "$(Resolve-Path .)\iad-practice\practice";
$files = Get-ChildItem -LiteralPath $root -Recurse -File -Filter *.ipynb;
foreach ($f in $files) {
  $rel = $f.FullName.Substring($root.Length).Replace("\\","/");
  $p = "/workspace$rel";
  docker exec dev-env-jupiter-notebook-1 jupyter nbconvert --to notebook --inplace --execute --ExecutePreprocessor.timeout=600 "$p"
}
```

3) Скопіювати результати до results/ (вже зроблено мною, але команда для повтору):

```powershell
New-Item -ItemType Directory -Force -Path "results" | Out-Null
Copy-Item -Path "iad-practice\practice\*" -Destination "results" -Recurse -Force
```

4) Закрити середовище за потреби:

```powershell
docker compose -f "iad-practice/dev-env/docker-compose.yml" down
```
