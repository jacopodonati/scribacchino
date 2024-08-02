# scribacchino.sh

`scribacchino.sh` è un semplice script per zsh che funge da SSG.  Prende i file contenuti in `src` e li compila con quelli salvati in `template` per poi scrivere il contenuto nella cartella `public`.  La base del sistema di templating è lo spazio unificatore (anche detto non-breaking space o `\xC2\xA0` in unicode).  In macOS si può fare con <kbd>opt</kbd>+<kbd>spazio</kbd>.  Se vuoi modificarlo, puoi farlo facilmente nello script cercando la stringa `\xC2\xA0`.

## template/ e partials/

La cartella `template` contiene i template.  Questi devono avere al loro interno la stringa ` contenuto ` (ossia la parola "contenuto" circondata da uno spazio unificatore prima e dopo).

Se il file contiene la stringa `  parziale.html  ` (ossia un doppio spazio unificatore prima e dopo), allora cercherà il file `parziale.html` nella cartella `template/partials`.  Al momento non è possibile inserire parziali all'interno di parziali.

I template possono inoltre contenere variabili che verranno sostituite in base al contenuto del file sorgente.  Queste hanno la forma ` nome_variabile `.

## src/

I file contenuti in `src` sono sorgenti e vengono compilati con il template segnalato a inizio file con un commento HTML del tipo `<!-- template: nome_template.html -->`.  Se non trova il template, dovrebbe usare il template `default.html`.

È inoltre possibile inserire variabili che verranno poi sostituite nel template.  Questa vanno segnalate sempre con un commento HTML del tipo `<!-- nome_variabile: valore_variabile -->`.

La gerarchia viene rispettata, perciò il file in `src/blog/post.html` genererà il file `public/blog/post.html`.
