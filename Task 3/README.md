## Задание 3. Оценка Data Encryption at Rest and In Transit

| Вид данных | Уровень чувствительности | Состояние данных | Основные риски / необходимость защиты | Как защищаем | Средства защиты **in transit** | Инструменты |
| --- | --- | --- | --- | --- | --- | --- |
| Критические медицинские данные (PHI) | Критический | at rest, in transit, in use | Врачебная тайна, ст. 13 323-ФЗ + ст. 10 152-ФЗ | Шифрование at rest + RBAC+ABAC + MFA | TLS 1.3 (все HTTP-сервисы 1С, Kafka, NiFi) | 1С:Медицина (RLS + теги)  
SQL Server TDE   
Windows FCI + DAC + BitLocker  
Exchange Transport Rules   
Keycloak |
| Персональные данные (PII) | Высокий | at rest, in transit | 152-ФЗ, утечки через почту и носители | Шифрование + RBAC + ABAC + MFA | TLS 1.3 + Exchange opportunistic TLS / forced TLS | 1С:Медицина (RLS + теги)  
SQL Server TDE   
Windows FCI + DAC + BitLocker  
Exchange Transport Rules  |
| Финансовые данные | Высокий | at rest, in transit | 152-ФЗ + 54-ФЗ + риск мошенничества | Tokenization + шифрование + строгий RBAC | TLS 1.3 + Exchange forced TLS для финансовых вложений | 1С:Бухгалтерия (RLS)  
SQL Server TDE  
BitLocker  
Exchange Transport Rules |
| Данные о сотрудниках | Высокий | at rest, in transit | 152-ФЗ (особые категории), внутренние утечки | Шифрование + RBAC (только HR) | TLS 1.3 + Exchange opportunistic / forced TLS | 1С:Бухгалтерия (RLS)  
SQL Server TDE   
Windows FCI + DAC + BitLocker  
Exchange Transport Rules  |
| Операционные / служебные данные | Средний | at rest | Коммерческая тайна, минимальные риски | NTFS-права + BitLocker | TLS 1.3 (если передача по сети) | BitLocker |
| Данные лабораторий (заказы и сырые результаты) | Критический | in transit, at rest | Врачебная тайна при передаче | End-to-end шифрование + проверка согласия | TLS 1.3 (обязательно) | 1С:Медицина (RLS + теги)  
SQL Server TDE   
Windows FCI + DAC + BitLocker |
| Логи и аудит событий | Высокий | at rest | Невозможность расследования инцидентов (ст. 19 152-ФЗ) | Append-only + шифрование + защита от изменения | TLS 1.3 (при передаче логов в центральный коллектор) | SQL Server Audit   
Windows Event Forwarding |