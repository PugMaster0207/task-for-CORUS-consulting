# task-for-CORUS-consulting
var invoice = {
"customer": "MDT", "performance": [
{"playId": "Гамлет", "audience": 55, "type": "tragedy" },
{"playId": "Ромео и Джульетта", "audience": 35, "type": "tragedy" },
{"playId": "Отелло", "audience": 40, "type": "comedy" } ] };
function statement(invoice, plays) {
let totalAmount = 0;
let volumeCredits = 0;
let result = 'Счет для ${invoice.customer}\n';
const format = new Inti.NumberFormat("ru-RU",{
style: "currency", currency: "RUB", minimumFractionDigits: 2 }).format;
for (let perf of invoice.performance) {
const play = plays[perf.playlD];
let thisAmount = 0;
switch (play.type) {
case "tragedy":
thisAmount = 40000;
if (perf.audience > 30) {
thisAmount += 1000 * (perf.audience - 30);
}
break;
case "comedy":
thisAmount = 30000;
if (perf.audience > 20) {
thisAmount += 10000 + 500 * (perf.audience - 20);
}
break;
thisAmount += 300 * perf.audience;
default:
throw new Error('неизвестный тип: ${play.type}');
}
// Добавление бонусов
volumeCredits += math.max(perf.audience - 30, 0);
// Дополнительный бонус за каждые 10 комедий
if ("comedy" === play.type) volumeCredits += math.floor(perf.audience / 10);
// Вывод строки счета
}
result += ' ${play.name}: ${format(thisAmount / 100)}';
result += ' (${perf.audience} мест)\n';
totalAmount += thisAmount;
result += 'Итого с вас $(format(totalAmount/100)}\n';
result += 'Вы заработали ${volumeCredits} бонусов\n';
return result;
}
