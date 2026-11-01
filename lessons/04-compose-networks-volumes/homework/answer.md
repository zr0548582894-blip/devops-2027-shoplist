1.  stats מגיע לbackend  בלי פורטס בגלל ששניהם נמצאים על אותו רשת DOKER ולכן הSTATS יכול לפנות אליו עי שם השירות
הדפדפן מגיע לbackend עי  פנייה ל Nginx והיא מקבלת את הבקשה ומעבירה אותה ל backend דרך docker
2.  כן המוצרים ישארו כי הם נשארים בnamed volume. לעומת זאת אם עושים -v המוצרים לא ישארו כי זה פקודה שמוחקת גם את הnamed volume.
3.  Bind Mount-עפ הניתוב שרואים ש../sql/init.sql הוא הקובץ מהמחשב, גם אם נשנה את  init.sql הנתונים ישמרו כי זה מורץ רק בפעם הראשונה ואחכ השינויים נמשרים בVOLUME.
4.  שם הרשת: docker_default
שם ה־Volume: docker_postgres-data
השמות נוצרו אוטומטית ע"י Docker Compose
5. שלב הProduction נשאר בImage הסופי  שבתוכו יש קבצי האתר קבצי הגדרות...
אין CMD כי: בתוך הIMAGE יש לנו כבר פקודת CMD 
למה stats לא צריך Multi-stage?
כי הוא מריץ ישירות את קובץ ה־JavaScript באמצעות Node.js
6. signle,multi מכילים את מה שצריך כדי להציג את האתר
לעומת זאת kitchem מכיל גם כלים המשמשים לבניית האתר.
7. כי היא ניגשת למה שהכי מתאים. הבקשה /api/stats מגיעה לstats כי היא מתאימה ל/api/stats וזה הניתוב הארוך ביותר המתאים. הבקשה /api/products מגיעה לbackend כי היא מתאימה לנתיב /api/ והלוכסן בסוף מעביר את הנתיב http://backend:5000/ עם products כלומר זה יראה כך: http://backend:5000/products
