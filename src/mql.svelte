<script>
    import Title from '@commons/title/m.svelte';
    import ContentContainer from '@commons/content-container/m.svelte';
    import Content from '@commons/content/m.svelte';
    import Form from '@commons/form/m.svelte';

    const formData = {
        style: 'mql',
        ':items': [
            {
                element: 'input',
                type: 'hidden',
                name: 'PGLANDPAGE',
                value: 'PGLandPage',
            },
            {
                element: 'page-url',
                name: 'SIGNLOC',
            },
            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                ':items': [
                    {
                        element: 'input',
                        classes: '6/12--tablet-up',
                        id: 'mcd-FNAME',
                        name: 'FNAME',
                        value: '',
                        analyticsName: 'first_name',
                        placeholder: 'First name',
                        options: {
                            required: true,
                            requiredMessage: 'First name is required.',
                            maxLength: 20,
                            maxLengthMessage:
                                'You can only enter up to 20 characters',
                        },
                    },
                    {
                        element: 'input',
                        classes: '6/12--tablet-up',
                        id: 'mcd-LNAME',
                        name: 'LNAME',
                        value: '',
                        analyticsName: 'last_name',
                        placeholder: 'Family name',
                        options: {
                            required: true,
                            requiredMessage: 'Last name is required.',
                            maxLength: 20,
                            maxLengthMessage:
                                'You can only enter up to 20 characters',
                        },
                    },
                ],
            },
            {
                element: 'input',
                id: 'mce-OPTIONAL-NAME',
                name: 'OPTIONAL-NAME',
                analyticsName: 'optional_name',
                placeholder: 'Preferred name (optional)',
                value: '',
                options: {
                    maxLength: 20,
                    maxLengthMessage: 'You can only enter up to 20 characters',
                },
            },
            {
                element: 'input',
                classes: 'm-input--mql__lasttextbox-margin',
                id: 'mce-EMAIL',
                name: 'EMAIL',
                analyticsName: 'email',
                placeholder: 'Email',
                value: '',
                options: {
                    required: true,
                    presets: ['email'],
                    message: 'Please enter a valid email.',
                    responsedErrorName: 'email',
                    maxLength: 80,
                    maxLengthMessage: 'You can only enter up to 80 characters.',
                },
            },

            {
                element: 'content-radio-group',
                title: 'I am',
                titleLevel: 3,
                name: 'RESIDENCY',
                items: [
                    {
                        name: 'domestic',
                        value: 'a+Domestic+student',
                        content:
                            '<h4>a Domestic student</h4><p>You are an Australian or New Zealand citizen, Australian permanent resident holder or humanitarian visa holder.</p>',
                    },
                    {
                        name: 'international',
                        value: 'an+International+student',
                        content:
                            '<h4>an international student</h4><p>You do not hold Australian or New Zealand citizenship and have not been granted permanent resident status in Australia.</p>',
                    },
                ],
                itemsClasses: '',
                itemClasses: '1/2--tablet-up',
                options: {
                    required: true,
                    requiredMessage:
                        'Please select if you are a domestic or international student.',
                },
            },
            {
                element: 'content-radio-group',
                title: 'I am interested in',
                titleLevel: 3,
                name: 'STUDY',
                items: [
                    {
                        name: 'underGraduate',
                        value: 'Undergraduate+coursework',
                        content:
                            '<h4>Undergraduate coursework</h4><p>An undergraduate degree, or bachelor’s degree, is the first degree you obtain at university.</p>',
                    },
                    {
                        name: 'postGraduate',
                        value: 'Postgraduate+coursework',
                        content:
                            '<h4>Postgraduate coursework </h4><p>Open to all graduates with a bachelor’s degree or, in some cases, equivalent work experience.</p>',
                    },
                    {
                        name: 'research',
                        value: 'Research',
                        content:
                            '<h4>Research</h4><p>For those wanting to pursue honours, masters by research or a PhD.</p>',
                    },
                ],
                itemClasses: '1/2--tablet-up',
                options: {
                    required: true,
                    requiredMessage: 'Please select your study area interest.',
                },
            },
            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                value: '',
                ':items': [
                    {
                        element: 'title',
                        text: 'I am a citizen of',
                        level: 3,
                        classes: '1/3--tablet-up',
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        element: 'input',
                        id: 'citizen',
                        name: 'CITIZEN',
                        classes: '2/3--tablet-up',
                        analyticsName: 'citizen',
                        placeholder: 'Citizen',
                        predictivePreset: 'countries',
                        value: '',
                        options: {
                            required: true,
                        },
                        conditions: [
                            {
                                name: 'show',
                                hiddenValue: 'Australia',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                    },
                                ],
                            },
                        ],
                    },
                ],
            },

            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                value: '',
                ':items': [
                    {
                        element: 'title',
                        text: ' I live in',
                        level: 3,
                        classes: '1/3--tablet-up',
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        element: 'grid',
                        wrapperClasses: '2/3--tablet-up',
                        ':items': [
                            {
                                element: 'checkbox-group',
                                name: 'LIVING_COUNTRY_IS_SAME',
                                classes:
                                    'm-content--no-margin-bottom m-grid__cell--min-full-width',
                                items: [
                                    {
                                        name: 'Same as citizenship',
                                        value: true,
                                    },
                                ],
                                value: '',
                                conditions: [
                                    {
                                        name: 'show',
                                        elements: [
                                            {
                                                name: 'RESIDENCY',
                                                value: 'an+International+student',
                                            },
                                        ],
                                    },
                                ],
                            },
                            {
                                element: 'input',
                                id: 'citizen',
                                name: 'COUNTRY',
                                classes: 'm-grid__cell--min-full-width',
                                analyticsName: 'citizen',
                                placeholder: 'Country',
                                predictivePreset: 'countries',
                                value: '',
                                options: {
                                    required: true,
                                },
                                conditions: [
                                    {
                                        name: 'same-as',
                                        from: 'CITIZEN',
                                        trigger: {
                                            name: 'LIVING_COUNTRY_IS_SAME',
                                            value: [true],
                                        },
                                    },
                                    {
                                        name: 'show',
                                        hiddenValue: 'N/A',
                                        elements: [
                                            {
                                                name: 'RESIDENCY',
                                                value: 'an+International+student',
                                            },
                                        ],
                                    },
                                ],
                            },
                        ],
                    },
                ],
            },

            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                value: '',
                ':items': [
                    {
                        element: 'title',
                        text: ' ',
                        level: 3,
                        classes: '1/3--tablet-up',
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        element: 'dropdown',
                        titleLevel: 4,
                        name: 'STATE',
                        classes: '2/3--tablet-up',
                        value: '',
                        analyticsName: 'state',
                        items: [
                            {
                                name: 'State/Territory',
                                value: '',
                                year: 'Select State',
                            },
                            {
                                name: 'Australian Capital Territory',
                                value: 'ACT',
                                analyticsValue: 2023,
                            },
                            {
                                name: 'New South Waless',
                                value: 'NSW',
                                analyticsValue: '2024Y',
                            },
                            {
                                name: 'Queensland',
                                value: 'Qld',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Victoria',
                                value: 'Vic',
                                analyticsValue: 'unsure',
                            },
                            {
                                name: 'Tasmania',
                                value: 'Tas',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Northern Territory',
                                value: 'NT',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'South Australia',
                                value: 'SA',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Western Australia',
                                value: 'WA',
                                analyticsValue: '2025Y',
                            },
                        ],
                        itemsWrapperClasses: '',
                        options: {
                            required: true,
                            requiredMessage:
                                'Please select you State/Territory.',
                        },
                        conditions: [
                            {
                                name: 'show',
                                hiddenValue: 'N/A',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                        elements: [
                                            {
                                                name: 'COUNTRY',
                                                value: 'Australia',
                                            },
                                        ],
                                    },
                                ],
                            },
                        ],
                   
                    },
                ],
            },

            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                value: '',
                ':items': [
                    {
                        element: 'title',
                        text: 'I live in',
                        level: 3,
                        classes: '1/3--tablet-up',
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'a+Domestic+student',
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        element: 'dropdown',
                        titleLevel: 4,
                        name: 'STATE',
                        classes: '2/3--tablet-up',
                        value: '',
                        analyticsName: 'state',
                        items: [
                            {
                                name: 'State/Territory',
                                value: '',
                                year: 'Select State',
                            },
                            {
                                name: 'Australian Capital Territory',
                                value: 'ACT',
                                analyticsValue: 2023,
                            },
                            {
                                name: 'New South Waless',
                                value: 'NSW',
                                analyticsValue: '2024Y',
                            },
                            {
                                name: 'Queensland',
                                value: 'Qld',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Victoria',
                                value: 'Vic',
                                analyticsValue: 'unsure',
                            },
                            {
                                name: 'Tasmania',
                                value: 'Tas',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Northern Territory',
                                value: 'NT',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'South Australia',
                                value: 'SA',
                                analyticsValue: '2025Y',
                            },
                            {
                                name: 'Western Australia',
                                value: 'WA',
                                analyticsValue: '2025Y',
                            },
                        ],
                        itemsWrapperClasses: '',
                        options: {
                            required: true,
                            requiredMessage:
                                'Please select you State/Territory.',
                        },
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'a+Domestic+student',
                                    },
                                ],
                            },
                        ],
                    },
                ],
            },

            {
                element: 'grid',
                classes: 'm-grid--vertical m-grid--horizontal--tablet-up',
                value: '',
                ':items': [
                    {
                        element: 'title',
                        text: 'Contact number',
                        level: 3,
                        classes: '1/3--tablet-up',
                        conditions: [
                            {
                                name: 'show',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                        elements: [
                                            {
                                                name: 'COUNTRY',
                                                value: 'China',
                                            },
                                        ],
                                    },
                                ],
                            },
                        ],
                    },
                    {
                        element: 'input',
                        id: 'contact-number',
                        name: 'CONTACT',
                        classes: '2/3--tablet-up',
                        analyticsName: 'contact',
                        placeholder: '+86',
                        value: '',
                        options: {
                            required: true,
                            requiredMessage: 'Please enter you contact number.',
                        },
                        conditions: [
                            {
                                name: 'show',
                                hiddenValue: 'N/A',
                                elements: [
                                    {
                                        name: 'RESIDENCY',
                                        value: 'an+International+student',
                                        elements: [
                                            {
                                                name: 'COUNTRY',
                                                value: 'China',
                                            },
                                        ],
                                    },
                                ],
                            },
                        ],
                    },
                ],
            },
            {
                element: 'checkbox-group',
                title: "I'm interested in studying",
                titleLevel: 3,
                analyticsName: 'area_of_interests',
                name: 'interests',
                itemsClasses: 'm-grid--vertical m-grid--horizontal--tablet-up',
                itemClass:
                    '1/1 1/2--tablet-up m-grid__cell m-grid__cell--full-width',
                checkboxBackgroundClass: 'm-checkbox-group--mql__option',
                checkboxCheckedClass: 'm-checkbox-group--mql__option--checked',
                checkboxTextClass: 'm-checkbox-group--mql__text',
                items: [
                    {
                        name: 'Arts and social sciences',
                        value: '5b4eecdffa',
                        analyticsValue: 'Arts and social sciences',
                    },
                    {
                        name: 'Architecture, design, and planning',
                        value: '5b962414b1',
                        analyticsValue: 'Architecture, design, and planning',
                    },
                    {
                        name: 'Business',
                        value: '0340ca2c44',
                        analyticsValue: 'Business',
                    },
                    {
                        name: 'Economics',
                        value: '29bbfb8d39',
                        analyticsValue: 'Economics',
                    },
                    {
                        name: 'Education and social work',
                        value: '5ba6bc38cb',
                        analyticsValue: 'Education and social work',
                    },
                    {
                        name: 'Engineering and computer science',
                        value: '8261ee5dd6',
                        analyticsValue: 'Engineering and computer science',
                    },
                    {
                        name: 'Law',
                        value: 'b0082161d9',
                        analyticsValue: 'Law',
                    },
                    {
                        name: 'Medicine and health',
                        value: '7e9566492b',
                        analyticsValue: 'Medicine and health',
                    },
                    {
                        name: 'Music',
                        value: 'abbd88fd91',
                        analyticsValue: 'Music',
                    },
                    {
                        name: 'Science',
                        value: '0323dbf040',
                        analyticsValue: 'Science',
                    },
                ],
            },
            {
                element: 'dropdown',
                title: 'I`d like to commence studies in',
                titleLevel: 3,
                name: 'YEAR',
                analyticsName: 'year',
                items: [
                    {
                        name: 'Select year',
                        value: '',
                        year: 'Select year',
                    },
                    {
                        name: '2023',
                        value: 2023,
                        analyticsValue: 2023,
                    },
                    {
                        name: '2024',
                        value: '2024Y',
                        analyticsValue: '2024Y',
                    },
                    {
                        name: '2025',
                        value: '2025Y',
                        analyticsValue: '2025Y',
                    },
                    {
                        name: 'Unsure',
                        value: 'unsure',
                        analyticsValue: 'unsure',
                    },
                ],
                itemsWrapperClasses: '',
                titleClasses: '3/5--tablet-up 2/3--sm-desk-up',
                itemClasses: '2/5--tablet-up 1/3--sm-desk-up',
                options: {
                    required: true,
                    requiredMessage:
                        'Please select which year you want to start studying.',
                },
            },
            {
                element: 'content-privacy-policy',
                classes: 'm-content--sm',
            },
            {
                element: 'grid',
                ':items': [
                    {
                        element: 'action',
                        name: 'Submit',
                        analytics: [
                            {
                                vendor: 'tealium',
                                defaultData: {
                                    tealium_event: 'main_lead_form_submission',
                                },
                            },
                        ],
                        request: {
                            vendor: 'MailChimp',
                            audienceId: '5e5ad51d76',
                            method: 'POST',
                            successful: {
                                actions: [
                                    {
                                        name: 'redirectTo',
                                        data: 'https://www.sydney.edu.au/study/stay-connected/thank-you.html',
                                    },
                                ],
                            },
                            fail: '',
                        },
                    },
                ],
            },
            {
                element: 'referrer',
                name: 'SIGNLOC',
            },
        ],
    };
</script>

<ContentContainer>
    <Content>
        <div class="m-grid">
            <div class="1/3--tablet-up m-grid__cell">
                it is a demo navigation part
            </div>
            <div class="2/3--tablet-up m-grid__cell">
                <Form modelData={formData} debugging={true} />
            </div>
        </div>
    </Content>
</ContentContainer>
