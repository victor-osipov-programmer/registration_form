<script setup>

</script>

<template>
    <Vueform :display-errors="false">
        <template #empty>
            <FormSteps>
                <FormStep
                    name="page0"
                    label="Страна"
                    :elements="[
                        'h1',
                        'country',
                        'language',
                        'another_country',
                        'link',
                    ]"
                    :labels="{
                        previous: 'Назад',
                        next: 'Вперёд',
                    }"
                />
                <FormStep
                    name="page1"
                    :elements="['age', 'special_case', 'registration_mentors']"
                    label="Возраст"
                    :conditions="[
                        [
                            ['country', 'in', ['Россия', 'Узбекистан']],
                            ['language', 'not_empty'],
                        ],
                    ]"
                    :labels="{
                        previous: 'Назад',
                        next: 'Вперёд',
                    }"
                />
                <FormStep
                    name="page2"
                    :elements="['participation', 'events']"
                    label="Участие"
                    :conditions="[
                        [
                            'age',
                            'in',
                            [
                                'Дошкольники (5-6 лет)',
                                'Младшая категория (7-9 лет)',
                                'Средняя категория (10-13 лет)',
                                'Старшая категория (14-17 лет)',
                            ],
                        ],
                    ]"
                    :labels="{
                        previous: 'Назад',
                        next: 'Вперёд',
                    }"
                />
                <FormStep
                    name="page3"
                    :elements="[
                        'target_user',
                        'mentor',
                        'participant_1',
                        'participant_2',
                        'participant_3',
                    ]"
                    label="Данные"
                    :labels="{
                        previous: 'Назад',
                        next: 'Оправить',
                    }"
                    :conditions="[
                        [
                            ['events', 'not_empty'],
                            [
                                'registration_mentors',
                                'in',
                                ['Соревнование наставников'],
                            ],
                        ],
                    ]"
                />
            </FormSteps>

            <FormElements>
                <StaticElement
                    name="h1"
                    tag="h1"
                    content="Приветственный текст"
                />
                <RadiogroupElement
                    name="country"
                    view="blocks"
                    :items="[
                        {
                            value: 'Россия',
                            label: 'Россия',
                            description: '',
                        },
                        {
                            value: 'Беларусь',
                            label: 'Беларусь',
                            description: '',
                        },
                        {
                            value: 'Казахстан',
                            label: 'Казахстан',
                            description: null,
                        },
                        {
                            value: 'Узбекистан',
                            label: 'Узбекистан',
                            description: null,
                        },
                        {
                            value: 'Иное',
                            label: 'Иное',
                            description: null,
                        },
                    ]"
                    :rules="['required']"
                    field-name="страна"
                />
                <RadiogroupElement
                    name="language"
                    view="tabs"
                    :items="[
                        {
                            value: 'Казахский',
                            label: 'Казахский',
                        },
                        {
                            value: 'Русский',
                            label: 'Русский',
                        },
                    ]"
                    label="Выберите язык"
                    :conditions="[['country', 'in', ['Казахстан']]]"
                    :rules="['required']"
                    field-name="язык"
                />
                <TextareaElement
                    name="another_country"
                    label="Укажите страну участия"
                    :conditions="[['country', 'in', ['Иное']]]"
                    field-name="другая страна"
                />
                <StaticElement
                    name="link"
                    content="Вам сюда - https://r-ed.by/fest2023/"
                    tag="a"
                    target="_blank"
                    href="https://r-ed.by/fest2023/"
                    :conditions="[['country', 'in', ['Беларусь']]]"
                    align="right"
                />
                <!-- <RadiogroupElement
                    name="target_mentor"
                    view="tabs"
                    :items="[
                        {
                            value: 'Наставник',
                            label: 'Наставник',
                        }
                    ]"
                /> -->
                <RadiogroupElement
                    name="target_user"
                    view="tabs"
                    :items="[
                        {
                            value: 'Участник 1',
                            label: 'Участник 1',
                        },
                        {
                            value: 'Участник 2',
                            label: 'Участник 2',
                        },
                        {
                            value: 'Участник 3',
                            label: 'Участник 3',
                        },
                        {
                            value: 'Наставник',
                            label: 'Наставник',
                        },
                    ]"
                    default="Участник 1"
                    size="sm"
                />
                <ObjectElement
                    name="mentor"
                    :conditions="[['target_user', 'in', ['Наставник']]]"
                >
                    <StaticElement name="p" tag="h4" content="Наставник" />
                    <TextElement
                        name="last_name"
                        :columns="{
                            container: 4,
                        }"
                        label="Фамилия"
                        :rules="['required']"
                    />
                    <TextElement
                        name="first_name"
                        label="Имя"
                        :columns="{
                            container: 4,
                        }"
                        :rules="['required']"
                    />
                    <TextElement
                        name="patronymic"
                        label="Отчество"
                        :columns="{
                            container: 4,
                        }"
                        :rules="['required']"
                    />
                    <TextElement
                        name="email"
                        input-type="email"
                        :rules="['nullable', 'required', 'email']"
                        label="Email"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="telegram_nickname"
                        label="Ник ТГ"
                        :columns="{
                            container: 6,
                        }"
                        :rules="['required']"
                    />
                    <TextElement
                        name="phone"
                        input-type="tel"
                        label="Телефон"
                        :rules="['required']"
                    />
                    <StaticElement name="divider" tag="hr" />
                    <MultifileElement
                        name="files"
                        label="Согласие на обработку перс. данных"
                        accept="pdf"
                        :drop="true"
                        :file="{
                            rules: ['mimes:pdf'],
                        }"
                        :rules="['size:2']"
                        :urls="{}"
                    />
                    <CheckboxElement
                        name="upload_files_later"
                        text="Загрузить позже"
                    />
                </ObjectElement>
                <ObjectElement
                    name="participant_1"
                    :conditions="[['target_user', 'in', ['Участник 1']]]"
                >
                    <StaticElement name="p" tag="h4" content="Участник 1" />
                    <TextElement
                        name="last_name"
                        :columns="{
                            container: 4,
                        }"
                        label="Фамилия"
                    />
                    <TextElement
                        name="first_name"
                        label="Имя"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <TextElement
                        name="patronymic"
                        label="Отчество"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <DateElement name="date_birth" label="Дата рождения" />
                    <TextElement
                        name="email"
                        input-type="email"
                        :rules="['nullable', 'email']"
                        label="Email"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="telegram_nickname"
                        label="Ник ТГ"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="phone"
                        input-type="tel"
                        label="Телефон"
                    />
                    <StaticElement name="divider" tag="hr" />
                    <TextElement name="text" label="Город" />
                    <TextElement
                        name="educational_institution"
                        label="Образовательное учреждение"
                    />
                </ObjectElement>
                <ObjectElement
                    name="participant_2"
                    :conditions="[['target_user', 'in', ['Участник 2']]]"
                >
                    <StaticElement name="p" tag="h4" content="Участник 2" />
                    <TextElement
                        name="last_name"
                        :columns="{
                            container: 4,
                        }"
                        label="Фамилия"
                    />
                    <TextElement
                        name="first_name"
                        label="Имя"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <TextElement
                        name="patronymic"
                        label="Отчество"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <DateElement name="date_birth" label="Дата рождения" />
                    <TextElement
                        name="email"
                        input-type="email"
                        :rules="['nullable', 'email']"
                        label="Email"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="telegram_nickname"
                        label="Ник ТГ"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="phone"
                        input-type="tel"
                        label="Телефон"
                    />
                    <StaticElement name="divider" tag="hr" />
                    <TextElement name="city" label="Город" />
                    <TextElement
                        name="educational_institution"
                        label="Образовательное учреждение"
                    />
                </ObjectElement>
                <ObjectElement
                    name="participant_3"
                    :conditions="[['target_user', 'in', ['Участник 3']]]"
                >
                    <StaticElement name="p" tag="h4" content="Участник 3" />
                    <TextElement
                        name="last_name"
                        :columns="{
                            container: 4,
                        }"
                        label="Фамилия"
                    />
                    <TextElement
                        name="first_name"
                        label="Имя"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <TextElement
                        name="patronymic"
                        label="Отчество"
                        :columns="{
                            container: 4,
                        }"
                    />
                    <DateElement name="date_birth" label="Дата рождения" />
                    <TextElement
                        name="email"
                        input-type="email"
                        :rules="['nullable', 'email']"
                        label="Email"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="telegram_nickname"
                        label="Ник ТГ"
                        :columns="{
                            container: 6,
                        }"
                    />
                    <TextElement
                        name="phone"
                        input-type="tel"
                        label="Телефон"
                    />
                    <StaticElement name="divider" tag="hr" />
                    <TextElement name="city" label="Город" />
                    <TextElement
                        name="educational_institution"
                        label="Образовательное учреждение"
                    />
                </ObjectElement>
                <RadiogroupElement
                    name="age"
                    view="blocks"
                    :rules="['required']"
                    :items="[
                        {
                            value: 'Дошкольники (5-6 лет)',
                            label: 'Дошкольники (5-6 лет)',
                            description: null,
                        },
                        {
                            value: 'Младшая категория (7-9 лет)',
                            label: 'Младшая категория (7-9 лет)',
                            description: null,
                        },
                        {
                            value: 'Средняя категория (10-13 лет)',
                            label: 'Средняя категория (10-13 лет)',
                            description: null,
                        },
                        {
                            value: 'Старшая категория (14-17 лет)',
                            label: 'Старшая категория (14-17 лет)',
                            description: null,
                        },
                    ]"
                    field-name="возраст"
                    :conditions="[
                        [
                            [
                                'special_case',
                                'not_in',
                                ['Регистрация наставников'],
                            ],
                            [
                                'registration_mentors',
                                'in',
                                ['Зарегистрировать команду детей'],
                            ],
                        ],
                    ]"
                />
                <RadiogroupElement
                    name="special_case"
                    view="blocks"
                    :items="[
                        {
                            value: 'Регистрация наставников',
                            label: 'Регистрация наставников',
                            description: '',
                        },
                        {
                            value: 'Категория для детей с ОВЗ',
                            label: 'Категория для детей с ОВЗ',
                            description: '',
                        },
                    ]"
                    label="Другое"
                />
                <RadiogroupElement
                    name="registration_mentors"
                    view="blocks"
                    :items="[
                        {
                            value: 'Соревнование наставников',
                            label: 'Соревнование наставников',
                            description: null,
                        },
                        {
                            value: 'Зарегистрировать команду детей',
                            label: 'Зарегистрировать команду детей',
                            description: null,
                        },
                    ]"
                    label="Регистрация наставников"
                    :conditions="[
                        ['special_case', 'in', ['Регистрация наставников']],
                    ]"
                    :rules="['required']"
                />
                <RadiogroupElement
                    name="participation"
                    view="tabs"
                    :items="[
                        {
                            value: 'Индивидуальное участие',
                            label: 'Индивидуальное участие',
                        },
                        {
                            value: 'Командное участие',
                            label: 'Командное участие',
                        },
                    ]"
                    default="Индивидуальное участие"
                    :rules="['required']"
                />
                <CheckboxgroupElement
                    name="events"
                    :rules="['required']"
                    field-name="мероприятия"
                    :items="[
                        {
                            value: 'Творческая категория',
                            label: 'Творческая категория',
                        },
                        {
                            value: 'Движение по линии',
                            label: 'Движение по линии',
                        },
                        {
                            value: 'Сумо',
                            label: 'Сумо',
                        },
                        {
                            value: 'Миссия &#34;Будущий инженер&#34;',
                            label: 'Миссия &#34;Будущий инженер&#34;',
                        },
                        {
                            value: 'Scratch Junior',
                            label: 'Scratch Junior',
                        },
                        {
                            value: 'Олимпиада «Старт в робототехнику»',
                            label: 'Олимпиада «Старт в робототехнику»',
                        },
                        {
                            value: 'Движение по линии DIY',
                            label: 'Движение по линии DIY',
                        },
                        {
                            value: 'Движение по линии Конструкторы',
                            label: 'Движение по линии Конструкторы',
                        },
                        {
                            value: 'Механическое сумо',
                            label: 'Механическое сумо',
                        },
                        {
                            value: 'Интеллектуальное сумо',
                            label: 'Интеллектуальное сумо',
                        },
                        {
                            value: 'Эстафета',
                            label: 'Эстафета',
                        },
                        {
                            value: 'Большое путешествие',
                            label: 'Большое путешествие',
                        },
                        {
                            value: 'Миссия &#34;Вселенная бесконечна&#34;',
                            label: 'Миссия &#34;Вселенная бесконечна&#34;',
                        },
                        {
                            value: 'Подводные роботы',
                            label: 'Подводные роботы',
                        },
                        {
                            value: '3Д моделирование',
                            label: '3Д моделирование',
                        },
                        {
                            value: 'Scratch',
                            label: 'Scratch',
                        },
                        {
                            value: 'Виртуальная реальность',
                            label: 'Виртуальная реальность',
                        },
                        {
                            value: 'БПЛА',
                            label: 'БПЛА',
                        },
                        {
                            value: 'Станки ЧПУ',
                            label: 'Станки ЧПУ',
                        },
                        {
                            value: 'Нейротехнологии',
                            label: 'Нейротехнологии',
                        },
                        {
                            value: 'Python',
                            label: 'Python',
                        },
                        {
                            value: 'Разработка игр',
                            label: 'Разработка игр',
                        },
                        {
                            value: 'Футбол',
                            label: 'Футбол',
                        },
                        {
                            value: 'Интернет вещей',
                            label: 'Интернет вещей',
                        },
                    ]"
                />
            </FormElements>

            <FormStepsControls />
        </template>
    </Vueform>
</template>
