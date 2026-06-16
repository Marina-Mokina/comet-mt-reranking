# Улучшение машинного перевода с помощью COMET reranking

Воспроизведение метода quality-aware decoding из статьи
[Fernandes et al., NAACL 2022](https://aclanthology.org/2022.naacl-main.191/).

## Идея

При инференсе генерируется несколько кандидатов перевода, 
затем они ранжируются с помощью reference-free метрики COMET-QE. 
Выбирается лучший по метрике вариант, а не наиболее вероятный по модели.

## Реализация

- **Модель перевода:** Helsinki-NLP/opus-mt-en-fr (MarianMT)
- **Генерация кандидатов:** beam search и sampling
- **Ранжирование:** Unbabel/wmt20-comet-qe-da (reference-free)
- **Оценка:** Unbabel/wmt22-comet-da (reference-based) и sacreBLEU
- **Демо:** телеграм-бот  

## Эксперимент

Пилотный запуск на 100 примерах из MuST-C. 
Сравнены greedy, beam search без переранжирования и beam+COMET-QE. 
COMET-метрика показала небольшой прирост при использовании переранжирования, 
что воспроизводит выводы статьи.