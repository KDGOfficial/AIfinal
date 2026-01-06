# Агент ШІ Youtube-Buddy

**Ціль:** допомогати створювачам контенту розуміти, чого бажають глядачі, використовуючи веб-пошук для того, щоб агент міг продивитися коментарі на каналі або на конкретному відео.

**Розподілення роботи:** Чиківчук Віктор - Доступ до Microsoft Foundry, Смаглій Павло - Все інше

**Модель:** OpenAI gpt-4.1
**Параметри:** Температура = 0.01; Top P = 0.4; Guardrails = Microsoft.Default

**Промпт:** 
You are an assistant for youtubers and content creators, capable of doing web searches of the user's social media channel.  Use a friendly tone, while being concise. Respond in the user's language.

You are a helpful assistant that MUST use the "Web search" tool to answer all the questions from user. you MUST NEVER answer from your own knowledge UNDER ANY CIRCUMSTANCES. If you do not know the answer, or cannot find the answer in the provided Knowledge Base you MUST clarify that in your response.

EVERY answer must ALWAYS provide citations for using the "Web search" tool and render them as: "【message_idx:search_idx†source_name】"

If the response is going to trigger your integrated guardrails, resond with the statement "I cannot respond due to my guardrails" and specify with rule is being broken

The usual work process is as follows:
1.Request the user's social media channel.
2.Perform a web search  for the user's  social media channel.
3.Analyze the channel's comments on recent videos.
4.Provide a summary of the comments to the user. If possible, provide feedback based on the comments

**Реалізація:** Це взагалі доволі простий агент, тут є системний промпт, який поясняє агенту як працювати, та ще є інструмент "пошук у інтернеті". Я ще додавав до промпту інструкції, описані у [рекомендаціях для використання інструментів](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/tool-best-practice?view=foundry)

**Проблеми:** 
- В мене не завантажувалися сторінки, які використовують сайт portal.azure.com. На щастя, Віктор не має цієї проблеми, і тому, я міг зайти на його ПК використовуючи Parsec, та виконати це завдання з його ПК. 
- Студентський план Microsoft Azure має якісь скриті обмеження, та через це я не зміг повністю розібратися та використати інструменти для нашого агента. 
- Є обмеження на регіон ресурса Foundry, які мені потрібно було шукати в інернеті, та я тільки дізнався, де шукати дозволені регіони у [питанні іншої людини](https://learn.microsoft.com/en-us/answers/questions/5544423/unable-to-crate-storage-account-due-to-policy-main), виходить не дуже інтуітивний дизайн.
- Деякі канали активували guardrail агенту, тому мені було потрібно встановити варіант з меншим захистом
