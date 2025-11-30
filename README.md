# deploy


To start the backend: 
docker compose up 



## Типовой рабочий процесс
1. Поднять Redis → ML-воркер → backend → frontend.
2. В UI загрузить CSV (столбцы text, src). Backend поставит задачу worker.process_file в Celery.
3. После обработки UI показывает кластеры (BERTopic + Qwen суммаризации), облако точек (UMAP), статистику тональности и список отзывов.

## Деплой
- Traefik роутер portfolio-analyzer настроен на fcdc5ae656279f7ee87b25ea.duckdns.org (HTTPS через Let’s Encrypt). Проверьте, что backend доступен на порту 8080 и сертификаты пишутся в ./letsencrypt/acme.json.
- Для production рекомендуем вынести фронт в отдельный контейнер/статический хост, а ML-воркер добавить в compose с тем же REDIS_URL.

## Тестирование
- Frontend: pnpm test (Vitest), pnpm lint.
- ML: python evaluate.py для расчета метрик по CSV; infer_test.py формирует submission.csv и test_probs.csv для проверки вывода.
