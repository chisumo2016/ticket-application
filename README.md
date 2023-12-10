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

# HELP TICKET PROJECT RESOURCE ROUTE
     - Create route   
        https://laravel.com/docs/10.x/controllers#resource-controllers

# HELP TICKET PROJECT CREATE TICKET
    - Create a commponent UI via cli
         php artisan make:component Textarea        
         php artisan make:component file-input

#  HELP TICKET PROJECT STORE TICKET WITH FILE 
    - Which route gonna submit
    - rule
            https://laravel.com/docs/10.x/validation#rule-file
    - Add the mass assgment in Ticket Model
    - ERROR
        SQLSTATE[HY000]: General error: 1364 Field 'user_id' doesn't have a default value
    - SOLN
        'user_id' => auth()->id()
    - Many ways to refactor 
            $ticket  = Ticket::create([
            'title' => $request->title,
            'description' => $request->description,
            'user_id' => auth()->id()
        ]);
