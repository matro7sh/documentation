# تقرير

يتم إنشاء التقرير من جانب العميل باستخدام هذه المكتبة

> [*docxtemplater*](https://www.npmjs.com/package/docxtemplater) 

:يتم توفير كل هذه المعلومات من قبل الخادم حتى تتمكن من تقديم طلب مثل هذا

`https://api.smersh.lan/api/missions/<ID>`

بالطبع سوف تحتاج إلى رمز المصادقة الخاص بك


: يمكنك استرداد هذا الرمز المميز باستخدام الأمر التالي



```c
curl --request POST \
  --url http://localhost:8000/authentication_token \
  --header 'Content-Type: application/json' \
  --data '{
	"username": "jenaye",
	"password": "jenaye"

}'
``` 

![report-preview](../img/preview-report.png){ width=40%, height=20%, align=right }

## أين يمكنني وضع نموذج دوكس الخاص بي ؟ 


: عليك أن تذهب إلى المجلد التالي

ثم قم بتسمية الملف

`Smersh.docx`.



>[line](https://github.com/matro7sh/Smersh/blob/d5c6a4397a35d786c72395073ea8186659cd5188/client/src/app/components/mission-single/mission-single.component.ts#L422)

## ما هي المتغيرات المستخدمة؟

فيما يلي قائمة جميع المتغيرات التي سيتم استخدامها لإنشاء التقرير

| startDate      | Start date of the mission                                                                                      |
|----------------|----------------------------------------------------------------------------------------------------------------|
| CLIENT_NAME    | Name of the customer                                                                                           |
| creds          | Bitwarden credentials  identifiers                                                                                  |
| classification | Type of report                                                                                                 |
| phone          | Phone number number                                                                                     |
| version        | Report version number                                                                                          |
| authors        |  List of pentesters assigned on the mission missioL                                                                 |
| state          | The status of the report                                                                                       |
| scope          | All the domain names and associated vulnerability as well as their criticality. |


: إذا كنت ترغب في إضافة مفتاح ، يمكنك ذلك ، ولكن عليك تحديث المتغير

`data`