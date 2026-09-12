# Adapter · Structural №1

**Статус:** ✅ залік 2026-09-12

## Формула полиці

Підключити **нове до старого** без переписування старого.

## Картка (5 рядків)

1. Перехідник: чужий API → наш інтерфейс.
2. Підключає нове без рефактору всього клієнтського коду.
3. + ізолює бруд чужого SDK в одному класі.
4. − зайвий шар; ризик розмноження адаптерів.
5. ≠ Facade (простий вхід до складної *своєї* підсистеми).

## Рамка

**Біль:** наш контракт і чужий SDK не стикуються.

**Питання**
1. Несумісні інтерфейси?
2. Чужий код не міняємо?
3. Хочемо лишити свій `charge` / `ship` / `debit`?

## Приклади

| Домен | Наш контракт | Чуже | Adapter |
|---|---|---|---|
| Fintech | `charge(amount)` | Stripe `createPaymentIntent` | `StripePaymentAdapter` |
| E-commerce | `ship(orderId)` | Nova Poshta API | `NovaPoshtaShippingAdapter` |
| Gambling | `debitWallet(...)` | provider wallet API | `ProviderWalletAdapter` |

## vs Facade

| Adapter | Facade |
|---|---|
| чужий інтерфейс → наш | простий вхід до купи модулів |
| Stripe під `charge()` | `pay()` → fraud + ledger + stripe |

## Тести (пройдено)

1. Stripe під `charge()` → **Adapter**
2. `pay()` → fraud+ledger+stripe → **Facade**
