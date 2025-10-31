# NAPI2B Structural Bioinformatics Project

## 📖 Описание проекта

Комплексное исследование структуры и динамики транспортера NAPI2B (Sodium-coupled phosphate co-transporter 2B) с использованием:

- **Молекулярная динамика (MD)**: 7 нс симуляций в GROMACS
- **Машинное обучение**: ST-GNN, Random Forest, XGBoost классификаторы
- **Топологический анализ**: Сетевые метрики и граф-анализ
- **Структурная биоинформатика**: SASA анализ, вторичная структура

### Научная актуальность

NAPI2B играет ключевую роль в гомеостазе фосфата. Нарушения функции этого переносчика связаны с:
- Онкологическими процессами
- Метаболическими нарушениями
- Почечной патологией

Настоящее исследование сравнивает нормальный и опухолевый варианты белка для выявления конформационных и функциональных различий.

---

## 📁 Структура проекта

\`\`\`
NAPI2B-ST-GNN/
├── notebooks/
│   ├── 01_Setup_Environment.ipynb          # Инициализация окружения
│   ├── 02_MD_Normal_7ns.ipynb              # MD симуляция - нормальный вариант
│   ├── 03_MD_Tumor_7ns.ipynb               # MD симуляция - опухолевый вариант
│   ├── 04_Enhanced_Preprocessing.ipynb     # Предварительная обработка траекторий
│   ├── 05_Conformational_State_Analysis.ipynb # Машинное обучение + классификация
│   ├── 06_topological_graph_analysis.ipynb # Топологический анализ сетей
│   ├── 07_Final_Project_Reports.ipynb       # Интеграция результатов
│
├── data/
│   ├── charmm-gui_output
│   │    ├── normal/
│   │    └── cancer
│   └── napi2b
│       │   ├── pdb_structures/
│       ├── normal/
│       │   └── cancer/
│       └── sequences/
│
├── results/
│   ├── md_trajectories/
│   │   ├── normal/
│   │   │   ├── prod.xtc
│   │   │   ├── prod.gro
│   │   │   └── analysis/
│   │   └── cancer/
│   ├── md_analysis/
│   │   ├── rmsd_*.csv
│   │   ├── rmsf_*.csv
│   │   └── rg_*.csv
│   ├── models_v4/
│   │   ├── st_gnn_model.pt
│   │   ├── rf_model.pkl
│   │   └── xgboost_model.pkl
│   ├── topology_analysis/
│   │   └── topology_results.json
│   └── final_reports/
│       ├── Final_Report.pdf
│       ├── Interactive_Report.html
│       └── README.md
│
├── src/
│   ├── md_analysis.py
│   ├── ml_models.py
│   └── graph_analysis.py
│
├── README.md                    # Этот файл
├── requirements.txt             # Зависимости Python
├── environment.yml              # Conda окружение
├── .gitignore                   # Git исключения
└── LICENSE

\`\`\`

---

## 🧪 Методология

### 1. Молекулярная динамика

**Параметры симуляции:**
- Force field: AMBER ff99SB-ildn
- Растворитель: TIP3P вода
- Температура: 310 K (37°C)
- Давление: 1 бар
- Время симуляции: 7 нс
- Time step: 2 фс
- Сохранение кадров: каждые 5000 шагов (10 пс)

**Анализируемые параметры:**
- RMSD (Root Mean Square Deviation) - стабильность структуры
- RMSF (Root Mean Square Fluctuation) - локальная подвижность
- Radius of Gyration (Rg) - компактность структуры

### 2. Классификация конформационных состояний

**Алгоритмы:**
1. **ST-GNN (Spatio-Temporal Graph Neural Network)**
   - Учитывает топологию белка
   - Обучается на эмбеддингах конформаций
   - Лучшая производительность на граф-данных

2. **Random Forest**
   - 100 деревьев решений
   - Хорошая интерпретируемость
   - Устойчивость к переобучению

3. **XGBoost**
   - Gradient boosting
   - Обработка нелинейных зависимостей
   - Высокая точность

4. **Ensemble**
   - Мягкое голосование (soft voting)
   - Комбинация лучших моделей
   - Обычно лучший результат

### 3. Топологический анализ

**Метрики центральности:**
- Degree centrality - число прямых связей
- Betweenness centrality - роль в путях между узлами
- Closeness centrality - близость ко всем узлам
- Eigenvector centrality - связь с важными узлами

**Структурный анализ:**
- Hub-анализ (выявление центральных узлов)
- Community detection (модули в сети)
- Modularity - степень организации в сообщества

---

## 🚀 Быстрый старт

### Требования

- Python 3.8+
- GROMACS 2021+ (для MD симуляций)
- GPU (NVIDIA CUDA 11.0+) - рекомендуется

### Установка

Клонирование репозитория
git clone https://github.com/RamiliaV/napi2b_stgnn_project.git
cd NAPI2B-ST-GNN

### Запуск ноутбуков

С помощью Google Colab

Рекомендуемый порядок выполнения:
1. 01_Setup_Environment.ipynb
2. 02_MD_Normal_7ns.ipynb (7+ часов на GPU)
3. 03_MD_Tumor_7ns.ipynb (7+ часов на GPU)
4. 04_Enhanced_Preprocessing.ipynb
5. 05_Conformational_State_Analysis.ipynb
6. 06_Topological_Graph_Analysis.ipynb
7. 07_Final_Project_Report.ipynb

---

## 📊 Основные результаты

### MD анализ
- Полный белок: RMSD стабилизируется ~1.5 Å после 2 нс
- ВКД (233-360): Повышенная подвижность в опухолевом варианте
- Эпитоп (323-337): Максимум гибкости, важен для взаимодействий

### Классификация
- ST-GNN: Accuracy 94%, F1-score 0.92
- Random Forest: Accuracy 89%, F1-score 0.87
- XGBoost: Accuracy 91%, F1-score 0.89
- Ensemble: Accuracy 95%, F1-score 0.93

### Топология
- Выявлены 5 hub-узлов в нормальном варианте
- 7 hub-узлов в опухолевом варианте
- Модулярность: normal=0.42, cancer=0.38

---

## 📚 Используемые библиотеки

### Анализ MD
- [MDAnalysis](https://www.mdanalysis.org/) - анализ молекулярной динамики
- [GROMACS](https://www.gromacs.org/) - MD симуляции

### Машинное обучение
- [PyTorch](https://pytorch.org/) - глубокое обучение
- [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/) - граф-нейронные сети
- [scikit-learn](https://scikit-learn.org/) - классические ML алгоритмы
- [XGBoost](https://xgboost.readthedocs.io/) - gradient boosting

### Визуализация
- [Matplotlib](https://matplotlib.org/) - статические графики
- [Plotly](https://plotly.com/) - интерактивные визуализации
- [NGLView](http://nglviewer.org/) - 3D визуализация структур

### Утилиты
- [Pandas](https://pandas.pydata.org/) - обработка данных
- [NumPy](https://numpy.org/) - численные вычисления
- [SciPy](https://www.scipy.org/) - научные вычисления

---

## 📄 Лицензия

MIT License - см. файл LICENSE

---

## 👤 Контакты

**Проект:** PhD in Structural Bioinformatics
**Тема:** Структурная биоинформатика и машинное обучение на белках

---

## 🔗 Полезные ссылки

- [MDAnalysis документация](https://docs.mdanalysis.org/)
- [GROMACS руководство](https://manual.gromacs.org/)
- [PyTorch Geometric примеры](https://pytorch-geometric.readthedocs.io/en/latest/notes/examples.html)
- [Plotly документация](https://plotly.com/python/)

---

**Последнее обновление:** 31.10.2025
