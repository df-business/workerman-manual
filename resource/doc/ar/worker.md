# فئة العامل (Worker)

في WorkerMan ، هناك فئتان مهمتان: Worker و Connection.

تستخدم فئة Worker للاستماع إلى المنافذ ويمكن لها تعيين وظيفة اندلاع حدث اتصال العميل، وظيفة استقبال رسائل الاتصال، وظيفة اندلاع حدث فصل الاتصال، وبالتالي تحقيق معالجة الأعمال.

يمكن تعيين عدد العمال (خاصية العداد) لنموذج العامل، حيث سيقوم العمل الرئيسي بتشعيع عدد العمليات الفرعية للعمل في نفس الوقت على استماع نفس المنفذ، واستقبال اتصالات العميل بتوازٍ ومعالجتها.