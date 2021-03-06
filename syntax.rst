Cuneiform Syntax Reference
==========================

This section gives a formal definition of the Cuneiform syntax. The entry point
of a Cuneiform program is the :ref:`syntax-script`.

All syntax diagrams have been generated using the
`Railroad Diagram Generator <http://www.bottlecaps.de/rr/ui>`_.

Complete Cuneiform syntax in EBNF::

    script       ::= statement+

    statement    ::= import
                   | define
                   | query

    query        ::= e ';'

    import       ::= 'import' "'...'" ';'

    define       ::= let-define
                   | fun-define

    let-define   ::= 'let' pattern '=' e ';'

    fun-define   ::= 'def' id '(' (id ':' type (',' id ':' type)* )? ')'
                     '->' type ( 'in' lang '*{ ... }*' | '{' define* e '}' )

    pattern      ::= id ':' type
                   | '<' id '=' pattern (',' id '=' pattern)* '>'

    lang         ::= 'Bash'
                   | 'Erlang'
                   | 'Java'
                   | 'Matlab'
                   | 'Octave'
                   | 'Perl'
                   | 'Python'
                   | 'R'
                   | 'Racket'

    type         ::= str-type
                   | file-type
                   | bool-type
                   | fun-type
                   | list-type
                   | record-type

    str-type     ::= 'Str'

    file-type    ::= 'File'

    bool-type    ::= 'Bool'

    fun-type     ::= ('Ntv' | 'Frn') '(' (id ':' type (',' id ':' type)* )? ')'
                     '->' type

    list-type    ::= '[' type ']'

    record-type  ::= '<' id ':' type (',' id ':' type)* '>'

    e            ::= var-e
                   | str-e
                   | file-e
                   | app-e
                   | bool-e
                   | cond-e
                   | list-e
                   | for-e
                   | fold-e
                   | record-e
                   | proj-e
                   | error-e


    var-e        ::= id

    str-e        ::= '"..."'

    file-e       ::= "'...'"


    app-e        ::= id '(' id '=' e (',' id '=' e)* ')'

    bool-e       ::= 'true'
                   | 'false'
                   | '(' e '==' e ')'
                   | 'not' e
                   | '(' e 'and' e ')'
                   | '(' e 'or' e ')'
                   | 'isnil' e

    cond-e       ::= 'if' e 'then' define* e 'else' define* e 'end'

    list-e       ::= '[' (e (',' e)*)? ':' type ']'
                   | '(' e '>>' e ')'
                   | '(' e '+' e ')'

    for-e        ::= 'for' id ':' type '<-' e (',' id ':' type '<-' e)*
                     'do' define* e ':' type 'end'

    fold-e       ::= 'fold' id ':' type '=' e ',' id ':' type '<-' e
                      'do' define* e 'end'

    record-e     ::= '<' id '=' e (',' id '=' e)* '>'

    proj-e       ::= '(' e '|' id ')'

    error-e      ::= 'error' '"..."' ':' type
    

.. toctree::
   :maxdepth: 2

   syntax-script
   syntax-statement
   syntax-define
   syntax-e
   syntax-type


