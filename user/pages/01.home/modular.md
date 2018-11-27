---
title: Caleb Perry
menu: home

onpage_menu: true
content:
    items: @self.modular
    order:
        by: default
        dir: asc
        custom:
            - _about
            - _resume
            - _portfolio
            - _call
            - _testimonials
            - _contact
form:
    name: my-nice-form
    action: /home
    fields:
        - name: name
          id: name
          label: Name
          classes: form-control form-control-lg
          placeholder: Enter your name
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          id: email
          classes: form-control form-control-lg
          label: Email
          placeholder: Enter your email address
          type: email
          validate:
            rule: email
            required: true

        - name: subject
          label: Subject
          classes: form-control form-control-lg
          size: long
          placeholder: Enter your subject
          type: text
          validate:
            requireed: false

        - name: message
          label: Message
          classes: form-control form-control-lg
          size: long
          placeholder: Enter your message
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Submit
          classes: btn btn-primary btn-block

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.subject|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thanks for reaching out! I'll respond as soon as possible :)
        - display: thankyou 
---
