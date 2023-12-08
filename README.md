#### Project Idea

    1: User can create a new help ticket 
    2: Admin cann reply on help ticket
    3: Admin can reject or resolve the ticket
    4: When admin update on the ticket then user will get one notification via email that ticket statusis updated
    5: User cab give ticket title and description
    6: User can upload a document like pdf or image

#### Table Structure Schema
    1: Tickets 
            - title (string)   { required}
            - description (text) { required}
            - status(open {default}, resolved , rejected) , Laravel level
            - attachments(string) { nullable}
            - user_id { required} filled by  laravel
            - status_changed_id { nullable}

    2: Replies 
            - body(text) { required} ,
            - user_id { required} filled by  laravel
            - ticket_id { required} filled by  laravel
    3: 
        
# HELP TICKET PROJECT CREATE MIGRATION MODEL CONTROLLER 
    - Migration 
            pa make:model Ticket -mrR     
    https://laravel.com/docs/10.x/migrations#columns
    https://laravel.com/docs/10.x/migrations#foreign-key-constraints
