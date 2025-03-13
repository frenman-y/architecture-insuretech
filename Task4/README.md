InsureTech Web получает предложения по ОСАГО через SSE от core-app, а заявки оформляются по REST. Core-app отправляет их
в osago-aggregator, который запрашивает страховые через REST API. Без ответа за 60 секунд предложение пропускается.

Circuit Breaker предотвращает блокировку core-app, Retry повторяет запросы при сбоях, а Rate Limiter защищает B2B-канал.
Osago-aggregator stateless и масштабируется через HPA. Для передачи данных между core-app и osago-aggregator
используется gRPC (streaming). Kafka не подходит из-за формата запрос–ответ.