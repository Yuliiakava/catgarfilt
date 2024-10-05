<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Градієнтний фон з анімацією</title>
    <style>
        body {
            height: 100vh;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(to bottom, #001f3f, #b03060); /* Темно-синій до темно-червоного */
            color: white;
            font-size: 2em;
            text-align: center;
            transition: background 0.5s;
            overflow: hidden; /* Забезпечує, що анімації не виходять за межі */
        }

        .emoji {
            position: absolute;
            font-size: 48px;
        }

        #cat {
            top: 10%;
            left: 10%;
            animation: moveCat 3s infinite alternate ease-in-out;
        }

        #hearts {
            bottom: 10%;
            right: 10%;
            animation: moveHearts 3s infinite alternate ease-in-out;
        }

        #heart {
            display: none; /* Ховаємо серце спочатку */
            font-size: 48px;
            position: absolute;
            bottom: 20%; /* Розміщуємо серце в нижній частині */
            left: 50%;
            transform: translateX(-50%); /* Центруємо серце */
            animation: fadeIn 1s; /* Додаємо анімацію для серця */
        }

        @keyframes moveCat {
            from {
                transform: translate(0, 0);
            }
            to {
                transform: translate(50px, 50px);
            }
        }

        @keyframes moveHearts {
            from {
                transform: translate(0, 0);
            }
            to {
                transform: translate(-50px, -50px);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <div id="text">Просто натискай на екран 🤍</div>

    <!-- Кіт та серця -->
    <div id="cat" class="emoji">🐈‍⬛🤍🐈‍⬛🤍🐈‍⬛🤍</div>
    <div id="hearts" class="emoji">🤍🐈‍⬛🤍🐈‍⬛🤍🐈‍⬛</div>
    <div id="heart" class="emoji">❤️</div> <!-- Додаємо червоне серце -->

    <script>
        const texts = [
                    "Хелоу котусик🐈‍⬛ ...",
                    "Ну що, здогадався, що це і як працює? 😎",
                    "Або я все ж таки підстрахуюсь і поясню? 🤔 Короче просто натискай на екран, коли прочитаєш повідомлення) ",
                    "Подумки обійняла! 🤗",
                    "Отже, все почалося з дня народження Тьоми. 🍰 🎉",
                    "Пам'ятаєш, як ти сказав, що такого ще не отримував? ",
                    "Я тоді серйозно задумалася, і тепер ось тобі… проєкт від мене, без поспіху!",
                    "І без зайвих багів, хоча… може один-два проскочать 😂",
                    "Я, звичайно, програмістка та ще та… колись хотіла писати код і бути крутою айтішницею.",
                    "Але не склалось! 😆 Якщо щось не працює — вибачай! ",
                    "Я перевірю все по максимуму, але це ж код, він, як і я, непередбачуваний! 🤣",
                    "Слухай, тут важливо не тицяти на екран бездумно, бо назад не повернешся. ",
                    "Ні, ну реально! 🙈 Тому, будь ласка, думай перед натисканням! 😜",
                    "Ти можещ тільки повернутись в самий початок натиснувши на синій надпис) ",
                    "Так, з чого б почати? Не можу зібрати думки докупи. ",
                    "Все завжди йде не так, коли я планую щось.",
                    "Ти зараз міг би сказати: «Знову ти там собі щось вигадала!» І був би правий) але ж так цікавіше)) ",
                    "Окей, давай почнемо з головнішого. Таксь ну саме перше буде те що ти неймовірно красивий! 😍",
                    "Заздрю тобі білою завістю через твої довгі вії, не ну реально чому в тебе вони густі та такі довгі? ",
                    "Бачиш як хотіла такі самі , що аж нарощення зробила )) ",
                    "Ти такий милий, коли спиш! 😇 В ті моменти хочеться загорнути тебе в ковдру і заховати від світу.",
                    "Але я ж добра, тому не буду 😜",
                    "Знаю, тобі важко говорити про емоції, але... чекай, НІ! Я очікую реакцію! ",
                    "Сподобається чи ні — хоча б напиши, що прочитав!",
                    "Уявляєш? Я написала стільки віршів, що можна збірку випускати! 📚 ",
                    "І майже всі вони про тебе, ну хіба це не круто? 😎 Після творчої кризи я знову почала писати",
                    "Я вже так звикла, що ти будиш мене вранці та говориш зі мною по дорозі на роботу. 🛌 ☕",
                    "Цікаво чи можна це вже вважати традицією ?) ",
                    "Знаєш, ти вмієш посміхатись очима! 👀",
                    "Не знаю, чи помічав ти це, але таке відчуття, ніби твої очі починають виглядати яскравіше ",
                    "Твій сміх заразний! 😂 Як тільки починаєш сміятися, я автоматично починаю теж! ",
                    "Слухай, я просто щаслива, що ти є у моєму житті. 💖",
                    "Тому що кому як не тобі я буду дзвонити та жалітись що люди дібіли?) ",
                    "До речі, ти геній сарказму та каламбурів! 🤣 ",
                    "Ой, здається, я знову пропустила рядок у коді... 🤦‍♀️ Ну не дурочка ж я?",
                    "Хоча, мій код це точно думає ",
                    "Ну що ж, завершила я свою хореографію під мою улюблену пісню. Думаю, ти здогадався, про яку йдеться! 💃🏻",
                    "До речі, ти залишив свій слід у моєму житті. Як мінімум завдяки Наруто!",
                    "Це дійсно одне із самих кращих аніме які я бачила🍥  ",
                    "Коли я приїду, приготую твій улюблений торт! 🎂",
                    "А потім будемо дивитись Гаррі Поттера і Гру Престолів під пледами з глінтвейном! 🍷",
                    "Я ж обіцяла то всьо подивитись із тобою )) ",
                    "Знаєш що? Я за тобою скучаю. І так, тепер живи з цією думкою! СКУЧАЮ! ",
                    "Але не думай що завжди)) Зі своїм теперешнім графіком я іноді їсти забуваю ",
                    "Скучаю за тим, як ми дивились аніме, і ти лежав у мене на животі або на нозі.",
                    "Твої обійми… твої обійми — це взагалі окрема тема! Обіцяю, що як тільки побачу тебе, обійму міцно міцно",
                    "От що мене зачепило найбільше — це кава, яку ти робив вранці! І шоколадки, які приносив! Ну просто ідеально! 🍫",
                    "Знаєш, чому я тебе так люблю? Бо ти робиш мій день яскравішим!  Навіть якщо це темні фарби",
                    "А пам'ятаєш як я приїала і зайшла в кімнату і ти злякався так що аж за серце схопився ?)) ",
                    "Зробила тобі шкарпетки, щоб ноги не мерзли. Хоча твої коментарі часом бувають такі холодні, що доведеться ще й рукавиці зв'язати! 🧦🧤",
                    "Все таки добре що я навчилась в'язати) ",
                    "Останнє тату — це, звісно, ти.",
                    "Що воно означає, не скажу, але ти точно вніс свій вклад у цей шедевр на моїй шкірі. ",
                    "Ти якось казав, що я занадто активна? 😏 Ну ось, сиджу спокійно вже цілих 10 хвилин, і це рекорд! 🤣 А все томц що не працює анімація🤣 ",
                    "Слухай, а якщо я тебе зараз задобрю смішними мемами і відосиками про аніме, ти приготуєш мені щось смачненьке? 🤭",
                    "З тобою завжди якось легше на душі, навіть коли день не задався 🫶",
                    "Доречі за носки, не дай Бог ти не будеш їх носити , я не знаю що з тобою зроблю😂",
                    "А ще я звикла до спокою з тобою,як би дивно це не звучало) ",
                    "Та знаю що моментами мене хочеться прибити, я вмію себе накрутити та як ти кажеш щось собі ото придумати,",
                    "АЛЕ я над цим працюю, і між іншим не сама, тому потерпи ще трошки)",
                    "До мене тільки зараз дійшло що я ось це все пишу і не зберігаю!!!",
                    "Так зараз збережу то всьо, і повернусь)) ",
                    "Ще не всьо, один момент) ",
                    "От тепер усьо) Їдемо далі)) ",
                    "Розрядимо атмосферу коротким віршиком) і ні я не питаю,я ставлю тебе перед фактом",
                    "Твій голос лунає, як шепіт вітрів,"
                    "Серед тиші ночей і далеких світів."
                    "Я мрію про мить, коли станеш ти тут,"
                    "І відстань між нами зникне, як сон.",
                    "Нічого не поробиш , я дівчина досить творча,",
                    "Але сподіваюсь що тобі сподобалось хоч трохи бо далі наступний",
                    "Пам'ятаєш я раніше писала за твою посмішку?",
                    "Так от",
                    "Твоя посмішка зігріває мене здалека,"
                    "Як сонце, що сходить крізь сутінки й туман."
                    "Я чекаю тебе, мій рідний, мій теплий,"
                    "Як квітка чекає свого теплого дня.",
                    "Якось так .... Тому я і прошу час від часу присилати фото або коротке відео, бачу тебе, і посміхаюсь",
                    "Думаю для маленького сюрпризу має стати ",
                    "Є багато того що я хочу тобі сказати, зробити , та подарувати.",
                    "Як мінімум може візит до окуліста , щоб ти частіше почав казати що я гарна, ладно жартую) Я пам'ятаю за твій віш-лист ",
                    "Але про це в іншій частині",
                    "Ти ж помітив цих  котів бігаючих по екрану? Конечно їх неможливо не помітити, походу треба спати лягати. Так от через них то вссьо так затягнулось",
                    "Це останні повідомлення які будуть тут... ",
                    "Та ми з тобою різні, хоч і є в чомусь схожість,",
                    "Хочу просто нагадати тобі ще раз що краса в очах того хто бачить,",
                    "В моїх очах ТИ особливий, ТИ гарний, ТИ став таким рідним за цей час ,чи якось так, я не знаю як тобі виразити правильніше свої почуття...",
                    "І якщо на те щоб ти зрозумів що ти для мене важливий треба буде декілька років,я почекаю) сподіваюсь що ракетою жесь не приєбє,такі реаллії нажаль",
                    "Але обіцяю буду максимально обережна, і буду дотримуватись всіх рекомендацій лікарів,",
                    "А ще можеш мене похвалити йде 6 день без кави , ну от не молодчинка))",
                    "Просто дякую тобі, що ти є, що ти справжній, і що терпиш мене , я це ціную, скучаю за тобою сонечко",
                    "Сподіваюсь що скоро зможу сказати то все дивлячись на тебе)",
                    "З теплими почуттями, Покахонтас🤍 ",
        ];

         let index = 0;
        const textElement = document.getElementById('text');
        const heartElement = document.getElementById('heart'); // Отримуємо серце

        document.addEventListener('click', () => {
            if (index < texts.length) {
                textElement.innerText = texts[index];
                index++;
            } else {
                textElement.innerText = ""; // Сховати текст
                heartElement.style.display = 'block'; // Показати серце
            }
        });
    </script>
</body>
</html>
