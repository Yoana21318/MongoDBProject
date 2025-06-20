# 🚗 MongoDB База Данни: `cars`

## 📦 Описание

Проектът съдържа MongoDB база данни на име `cars`, с една основна колекция също на име `cars`, която съхранява информация за различни модели автомобили. Базата данни е предназначена за демонстриране на CRUD операции и агрегационни заявки.

---

## 📂 Структура на колекцията

### Колекция: `cars`

Всеки документ в колекцията представлява автомобил със следните полета:

| Поле       | Тип              | Описание                            |
|------------|------------------|-------------------------------------|
| `model`    | `string`         | Модел на автомобила                 |
| `brand`    | `string`         | Марка                               |
| `year`     | `int`            | Година на производство              |
| `price`    | `int`            | Цена в USD                          |
| `features` | `array<string>`  | Екстри                              |
| `specs`    | `object`         | Спецификации: `engine`, `fuel`, `hp` |

#### Примерен документ:
```json
{
  "model": "Camry",
  "brand": "Toyota",
  "year": 2023,
  "price": 28000,
  "features": ["lane assist", "backup camera"],
  "specs": { "engine": "2.5L", "fuel": "hybrid", "hp": 203 }
}
📥 Вмъкване на данни
Данните се вмъкват чрез файл insert.js, съдържащ 10 автомобилни записа. Файлът може да се стартира с:

bash
Copy
Edit
mongosh < insert.js
Уверете се, че сте в правилната база данни:

js
Copy
Edit
use cars
🔍 Основни заявки (CRUD)
Извличане на всички документи:
js
Copy
Edit
db.cars.find()
Филтриране по марка:
js
Copy
Edit
db.cars.find({ brand: "Toyota" })
Филтриране по марка и година:
js
Copy
Edit
db.cars.find({ brand: "Ford", year: { $gte: 2020 } })
Актуализация на цена:
js
Copy
Edit
db.cars.updateOne({ model: "Civic" }, { $set: { price: 21000 } })
Изтриване на документ:
js
Copy
Edit
db.cars.deleteOne({ model: "Yaris" })
📊 Примери за агрегации
Средна цена по марка:
js
Copy
Edit
db.cars.aggregate([
  { $group: { _id: "$brand", averagePrice: { $avg: "$price" } } }
])
Брой автомобили по марка:
js
Copy
Edit
db.cars.aggregate([
  { $group: { _id: "$brand", count: { $sum: 1 } } }
])
Сортиране на автомобили по цена (низходящо):
js
Copy
Edit
db.cars.aggregate([
  { $sort: { price: -1 } }
])
⚙️ Изисквания
MongoDB инсталация (напр. MongoDB Compass или mongosh)

insert.js за първоначално вмъкване на данни

queries.js за заявки и тестове
