#### Project Idea

    1: User can create a new help ticket 
    2: Admin AND user can reply on help ticket
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

# HELP TTICKET PROJECT PASS VIEW VARIABLE
    - Display all tickets onn index page 
    - Various way to data on the view
        1: 
        $tickets = Ticket::all();
        return view('ticket.index')->with('tickets', $tickets);
        
        2:

        $tickets = Ticket::all();
        return view('ticket.index', ['tickets' => $tickets]);

        3:
        $tickets = Ticket::all();
        return view('ticket.index', compact('tickets'));
    - Show single ticket
        <a href="{{ route('ticket.show') }}"></a>
        Missing required parameter for [Route: ticket.show] [URI: ticket/{}] [Missing parameter: ].

# HELP TICKET PROJECT ROUTE MODEL BINDING
        https://laravel.com/docs/10.x/folio#route-model-binding

# HELP TICKET PROJECT DELETE MODEL
    Add the button 
    Add  the form to delete 
    Add logic 
# HELP TICKET PROJECT - EDIT AND UPDATE
    - Create a new ui called edit
    - Create button for edit in show ui
    - Create a logic inside the TicketConntroller
    - Add logic inside the UpdateRequest
    - Apply DRY 

# HELP TICKET PROJECT - ADMIN ACCESSOR
    - Work on admin section 
    - how do u define is_admin
    - we can create a simple accessor  in our user moodel
        tinnker
        $user = User::whereEmail('bchisumo@yahoo.com)->first
        $user->isAdmin
    - Approve or Reject button

# HELP TICKET PROJECT - REQUEST EXCEPT RULE IN
    In approve and reject button , we should have two forms
    Update the status of tthe  ticket
    Ticket MModel
    We need the Approve and Reject to be for admin only

# HELP TICKET PROJECT - LARAVEL NOTIFICATION
    - Trigger notofication in  update method
        https://laravel.com/docs/10.x/notifications#main-content
    - php artisan make:notification TicketUpdattedNotification  
    - Various channnel to send the notification
    https://laravel.com/docs/10.x/notifications#mail-notifications

# HELP TICKET PROJECT - HAS MANY RELATIONSHIP
    - Open the .env
    - we can use mail trap / Beyond code
        https://laravel.com/docs/10.x/eloquent-relationships#main-content
