# # Ключ аутентификации-CSHARP-Пример
Пример проверки подлинности ключа на C# для https://keyauth.ru система аутентификации.

## **Ошибки**

Если пример по умолчанию, не добавленный в ваше программное обеспечение, работает неправильно, пожалуйста, присоединяйтесь к серверу Discord https://discord.gg/keyauth и отправьте сообщение о проблеме в канале `#ошибки`.

Однако мы **НЕ** предоставляем поддержку для добавления ключа аутентификации в ваш проект. Если вы не можете в этом разобраться, вам следует воспользоваться Google или YouTube, чтобы узнать больше о языке программирования, на котором вы хотите продавать программу.

## Лицензия на авторское право

Аутентификация ключа осуществляется по лицензии **Elastic License 2.0**

* Вы не имеете права предоставлять программное обеспечение третьим лицам в качестве размещенного или управляемого
сервиса, если сервис предоставляет пользователям доступ к какому-либо существенному набору
функций программного обеспечения.

* Вы не имеете права перемещать, изменять, отключать или обходить функциональные возможности лицензионного ключа
в программном обеспечении, а также вы не имеете права удалять или скрывать какие-либо функциональные
возможности программного обеспечения, защищенные лицензионным ключом.

* Вы не имеете права изменять, удалять или скрывать какие-либо уведомления о лицензировании, авторских правах или другие уведомления
лицензиара в программном обеспечении. Любое использование товарных знаков лицензиара регулируется
применимым законодательством.

Благодарим вас за ваше согласие, мы усердно работаем над разработкой Key Auth и не одобряем нарушения ваших авторских прав.


## Проблемы с подключением клиентов?

Это распространено среди всех систем аутентификации. Запутывание программы приводит к ложным срабатываниям антивирусных сканеров, и с учетом масштаба проверки подлинности ключа это воспринимается как вредоносный домен. Итак,`keyauth.ru " были заблокированы многими интернет-провайдерами. для панели мониторинга, панели реселлера, панели клиента используйте `keyauth.ru `

Для API, `keyauth.ru "не сработает, потому что я намеренно заблокировал его там, так что `keyauth.ru "также не блокируется. Итак, вам следует создать свой собственный домен и следовать этому обучающему видео https://www.youtube.com/watch?v=a2SROFJ0eYc . В обучающем видео показано, как создать доменное имя на 100% бесплатно, если вы не хотите его приобретать.

## Определение экземпляра `KeyAuthApp`

Визит https://keyauth.ru/app / и выберите свое приложение, затем перейдите на вкладку **C#**

Он предоставит вам код, который вы должны заменить в файле `Program.cs` (или файле `Login.cs`, если используете пример формы).

```cs
public static api KeyAuthApp = new api(
    name: "example",
    ownerid: "JjPMBVlIOd",
    secret: "db40d586f4b189e04e5c18c3c94b7e72221be3f6551995adc05236948d1762bc",
    version: "1.0"
);
```

## Инициализировать приложение

Вы должны вызвать эту функцию перед использованием любой другой функции проверки подлинности ключа. В противном случае другая функция аутентификации по ключу не будет работать.

```cs
KeyAuthApp.init();
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
```

## Отображение информации о приложении

```cs
KeyAuthApp.fetchStats();
Console.WriteLine("\n Application Version: " + KeyAuthApp.app_data.version);
Console.WriteLine(" Customer panel link: " + KeyAuthApp.app_data.customerPanelLink);
Console.WriteLine(" Number of users: " + KeyAuthApp.app_data.numUsers);
Console.WriteLine(" Number of online users: " + KeyAuthApp.app_data.numOnlineUsers);
Console.WriteLine(" Number of keys: " + KeyAuthApp.app_data.numKeys);
```

## Проверьте правильность сеанса

Используйте это, чтобы узнать, вошел ли пользователь в систему или нет.

```cs
KeyAuthApp.check();
Console.WriteLine($" Current Session Validation Status: {KeyAuthApp.response.message}");
```

## Проверить статус черного списка

Проверьте, внесен ли HWID или IP-адрес в черный список. Вы можете добавить это, если хотите, просто чтобы убедиться, что никто не сможет открыть вашу программу менее чем на секунду, если они занесены в черный список. Однако, если вы не возражаете, чтобы пользователь, занесенный в черный список, пользовался программой в течение нескольких секунд, пока он не попытается войти в систему и зарегистрироваться, и вы заботитесь о том, чтобы программа была максимально быстрой для ваших пользователей, тогда вам не следует использовать эту функцию. Если пользователь, внесенный в черный список, попытается войти в систему / зарегистрироваться, сервер проверки подлинности ключей проверит, внесен ли он в черный список, и, если да, отклонит вход. Таким образом, функция проверки черного списка - это просто вспомогательная функция, которая необязательна.

```cs
if(KeyAuthApp.checkblack()) {
    Environment.Exit(0);  // terminate program if user blacklisted.
}
```

## Войдите в систему с помощью имени пользователя/пароля

```cs
string username;
string password;
Console.WriteLine("\n\n Enter username: ");
username = Console.ReadLine();
Console.WriteLine("\n\n Enter password: ");
password = Console.ReadLine();
KeyAuthApp.login(username, password);
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
```

## Зарегистрируйтесь с помощью имени пользователя/ пароля /ключа

```cs
string username, password, key, email;
Console.Write("\n\n Enter username: ");
username = Console.ReadLine();
Console.Write("\n\n Enter password: ");
password = Console.ReadLine();
Console.Write("\n\n Enter license: ");
key = Console.ReadLine();
Console.Write("\n\n Enter email (just press enter if none): ");
email = Console.ReadLine();
KeyAuthApp.register(username, password, key, email);
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
```

## Обновить имя пользователя/ключ

Используется для того, чтобы пользователь мог добавить дополнительное время к своей учетной записи, запросив новый ключ.

> **Предупреждение**
> Для обновления учетной записи пароль не требуется. Таким образом, в отличие от функций входа в систему, регистрации и лицензирования - вы не должны **** входить в систему пользователя после успешного обновления.

```
string username;
string password;
string key;
Console.WriteLine("\n\n Enter username: ");
username = Console.ReadLine();
Console.WriteLine("\n\n Enter license: ");
key = Console.ReadLine();
KeyAuthApp.upgrade(username, key);
// don't proceed to app, user hasn't authenticated yet.
Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
Thread.Sleep(2500);
Environment.Exit(0);
```

## Войдите в систему, используя только лицензионный ключ

Пользователи могут использовать эту функцию, если их лицензионный ключ никогда ранее не использовался и если он использовался ранее. Поэтому, если вы планируете просто разрешить пользователям использовать ключи, вы можете удалить функции входа в систему и регистрации из своего кода.

```cs
string key;
Console.WriteLine("\n\n Enter license: ");
key = Console.ReadLine();
KeyAuthApp.license(key);
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
```

## Войдите в систему с помощью веб-загрузчика

Попросите ваших пользователей войти в систему через веб-сайт. Обучающее видео здесь https://www.youtube.com/watch?v=9-qgmsUUCK4 вы также можете использовать свой собственный домен для клиентской панели, https://www.youtube.com/watch?v=iHQe4GLvgaE

```cs
KeyAuthApp.web_login();

Console.WriteLine("\n Waiting for button to be clicked");
KeyAuthApp.button("close");
```

## Забыли пароль

Разрешите пользователям вводить данные своей учетной записи и получать электронное письмо для сброса пароля.

```cs
string username, email;
Console.Write("\n\n Enter username: ");
username = Console.ReadLine();
Console.Write("\n\n Enter email: ");
email = Console.ReadLine();
KeyAuthApp.forgot(username, email);
// don't proceed to app, user hasn't authenticated yet.
Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
Thread.Sleep(2500);
Environment.Exit(0);
```

## Пользовательские данные

Отображать информацию для текущего пользователя, вошедшего в систему.

```cs
Console.WriteLine("\n User data:");
Console.WriteLine(" Username: " + KeyAuthApp.user_data.username);
Console.WriteLine(" IP address: " + KeyAuthApp.user_data.ip);
Console.WriteLine(" Hardware-Id: " + KeyAuthApp.user_data.hwid);
Console.WriteLine(" Created at: " + UnixTimeToDateTime(long.Parse(KeyAuthApp.user_data.createdate)));
if (!String.IsNullOrEmpty(KeyAuthApp.user_data.lastlogin)) // don't show last login on register since there is no last login at that point
    Console.WriteLine(" Last login at: " + UnixTimeToDateTime(long.Parse(KeyAuthApp.user_data.lastlogin)));
Console.WriteLine(" Your subscription(s):");
for (var i = 0; i < KeyAuthApp.user_data.subscriptions.Count; i++)
{
    Console.WriteLine(" Subscription name: " + KeyAuthApp.user_data.subscriptions[i].subscription + " - Expires at: " + UnixTimeToDateTime(long.Parse(KeyAuthApp.user_data.subscriptions[i].expiry)) + " - Time left in seconds: " + KeyAuthApp.user_data.subscriptions[i].timeleft);
}
```

## Проверьте имя пользователя для подписки

Если вы хотите запретить доступ к частям вашего приложения только определенным пользователям, у вас может быть несколько подписок с разными именами. Затем, когда вы создадите лицензии, соответствующие уровню этой подписки, пользователи, которые используют эти лицензии, получат подписку с названием подписки, соответствующим уровню используемого ими лицензионного ключа. Функция `Sub Exist` находится в файле `Program.cs`

```cs
if (SubExist("default"))
{
    Console.WriteLine(" Default Subscription Exists");
}
// See if another sub exists with name 
if (SubExist("premium"))
{
    Console.WriteLine(" Premium Subscription Exists");
}
```

## Показать список онлайн-пользователей

```cs
var onlineUsers = KeyAuthApp.fetchOnline();
if (onlineUsers != null)
{
    Console.Write("\n Online users: ");
    foreach (var user in onlineUsers)
    {
        Console.Write(user.credential + ", ");
    }
    Console.WriteLine("\n");
}
```

## Переменные приложения

Строка, которая хранится на стороне сервера Key Auth. На панели мониторинга вы можете выбрать для каждой переменной аутентификацию (доступ могут получить только зарегистрированные пользователи) или не аутентификацию (любой пользователь может получить доступ до входа в систему). Они являются глобальными и статичными для всех пользователей, в отличие от пользовательских переменных, которые будут рассмотрены ниже в этом разделе.

```cs
string appvar = KeyAuthApp.var("variableNameHere");
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
else
    Console.WriteLine("\n App variable data: " + appvar);
```

## Пользовательские переменные

Пользовательские переменные - это строки, хранящиеся на стороне сервера Key Auth. Они специфичны для пользователей. Их можно установить на панели мониторинга на вкладке "Пользователи", через SellerAPI или через ваш загрузчик, используя приведенный ниже код. "discord" - это имя пользовательской переменной, по которому вы извлекаете пользовательскую переменную. `test#0001` - это данные переменной, которые вы получаете при извлечении пользовательской переменной.

```cs
KeyAuthApp.setvar("discord", "test#0001");
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
else
    Console.WriteLine("\n Successfully set user variable");
```

И вот как вы извлекаете пользовательскую переменную:

```cs
string uservar = KeyAuthApp.getvar("discord");
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
else
    Console.WriteLine("\n User variable value: " + uservar);
```

## Журналы приложений

Может использоваться для регистрации данных. Хорошо подходит для предупреждений об отладке и, возможно, для отладки ошибок. Если вы настроите Discord webhook в настройках приложений панели мониторинга, он будет отправлять сообщения журнала на ваш Discord webhook, а не сохранять их на сайте. Рекомендуется установить Discord webhook, так как логи на сайте удаляются через 1 месяц после отправки.

Вы можете использовать функцию регистрации до входа в систему и после входа в систему.

```cs
KeyAuthApp.log("hello I wanted to log this");
```

## Забанить пользователя

Заблокируйте пользователя и внесите в черный список его HWID и IP-адрес. Хорошая функция для вызова, если вы используете защиту от отладки и обнаружили попытку вторжения.

Функция работает только после входа в систему.

```cs
KeyAuthApp.ban();
```

## Забанить пользователя (с указанием причины)

Заблокируйте пользователя и внесите в черный список его HWID и IP-адрес. Хорошая функция для вызова, если вы используете защиту от отладки и обнаружили попытку вторжения.

Функция работает только после входа в систему.

Параметром reason будет причина запрета, отображаемая пользователю при попытке входа в систему и видимая на панели управления KeyAuth.

```cs
KeyAuthApp.ban("Don't try to crack my loader, cunt.");
```

## Веб-хуки на стороне сервера

Обучающее видео https://www.youtube.com/watch?v=ENRaNPPYJbc

> **Примечание**
> Прочитайте документацию для веб-подключений KeyAuth здесь https://keyauth.readme.io/reference/introduction

Безопасно отправляйте HTTP-запросы по URL-адресам, не допуская утечки URL-адреса в вашем приложении. Вам обязательно следует использовать, если вы хотите отправлять запросы в SellerAPI из своего приложения, в противном случае, если вы этого не сделаете, вы передадите свой ключ продавца всем. И тогда кто-то может испортить ваше приложение.

1-й пример - это как отправить запрос без данных POST. просто запрос GET на URL-адрес. `7kR0UedlVI` - это идентификатор веб-узла, `https://keyauth.ru/api/seller/?sellerkey=sellerkeyhere&type=black ` - это то, что вы должны указать в качестве конечной точки webhook на панели мониторинга. Это та часть, которую вы не хотите, чтобы пользователи видели. И тогда у вас есть `&ip=1.1.1.1&hwid=abc` в вашем программном коде, который будет добавлен к конечной точке webhook на сервере keyauth, а затем запрос будет отправлен.

2-й пример включает в себя данные post. это данные формы. это пример запроса к KeyAuth API. `7kR0UedlVI` - это идентификатор веб-узла, `https://keyauth.ru/api/1.2 /` - это конечная точка webhook.

3-й пример включал данные post, хотя это JSON. Это пример запроса к Discord webhook `7kR0UedlVI` - это идентификатор webhook, `https://discord.com/api/webhooks /...` - это конечная точка webhook.

```cs
// example to send normal request with no POST data
string resp = KeyAuthApp.webhook("7kR0UedlVI", "&ip=1.1.1.1&hwid=abc");

// example to send form data
resp = KeyAuthApp.webhook("7kR0UedlVI", "", "type=init&name=test&ownerid=j9Gj0FTemM", "application/x-www-form-urlencoded");

// example to send JSON
resp = KeyAuthApp.webhook("7kR0UedlVI", "", "{\"content\": \"webhook message here\",\"embeds\": null}", "application/json"); // if Discord webhook message successful, response will be empty

if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
else
    Console.WriteLine("\n Response received from webhook request: " + resp);
```

## Загрузить файл

> **Примечание**
> > Ознакомьтесь с документацией по ключевым файлам аутентификации здесь https://keyauth.readme.io/reference/introduction

Обеспечьте безопасность файлов, предоставив KeyAuth ссылку для скачивания вашего файла на панели управления KeyAuth. Убедитесь, что это прямая ссылка для скачивания (как только вы перейдете по ссылке, она начнет загружаться без вашего нажатия на что-либо). Функция загрузки KeyAuth предоставляет байты, а затем вы сами решаете, что с ними делать. В этом примере показано, как записать его в файл с именем `text.txt ` в той же папке, что и программа, хотя вы могли бы выполнить ее с помощью RunPE или чего угодно еще.

`385624` - это идентификатор файла, который вы получаете на панели мониторинга после добавления файла.

```cs
byte[] result = KeyAuthApp.download("385624");
if (!KeyAuthApp.response.success)
{
    Console.WriteLine("\n Status: " + KeyAuthApp.response.message);
    Thread.Sleep(2500);
    Environment.Exit(0);
}
else
    File.WriteAllBytes(Directory.GetCurrentDirectory() + "\\test.txt", result);
```

## Каналы чата

Разрешите пользователям общаться между собой в вашей программе.

Пример из примера формы о том, как извлекать сообщения чата.

```cs
var messages = Login.KeyAuthApp.chatget("chatChannelNameHere");
if (messages == null)
{
    dataGridView1.Rows.Insert(0, "KeyAuth", "No Chat Messages", UnixTimeToDateTime(DateTimeOffset.Now.ToUnixTimeSeconds()));
}
else
{
    foreach (var message in messages)
    {
        dataGridView1.Rows.Insert(0, message.author, message.message, UnixTimeToDateTime(long.Parse(message.timestamp)));
    }
}
```

Пример из формы example о том, как отправить сообщение в чате.

```cs
if (Login.KeyAuthApp.chatsend(chatmsg.Text, chatchannel))
{
    dataGridView1.Rows.Insert(0, Login.KeyAuthApp.user_data.username, chatmsg.Text, UnixTimeToDateTime(DateTimeOffset.Now.ToUnixTimeSeconds()));
}
else
    chatmsg.Text = "Status: " + Login.KeyAuthApp.response.message;
```
