# NOTIFYme

NOTIFYme est une bibliothèque Go simple conçue pour envoyer des notifications
via divers canaux tels que l'e-mail, ntfy.sh, etc., vous permettant également
d'envoyer un message à plusieurs canaux de notification simultanément.

## Installation

Pour installer NOTIFYme, vous pouvez utiliser la commande suivante :

```bash
go get github.com/socme-project/notifyme
```

## Utilisation

Pour utiliser NOTIFYme, vous devez importer le package dans votre code Go :

```go
import "github.com/socme-project/notifyme"
```

Vous pouvez ensuite créer un nouveau notificateur et envoyer des notifications
via différents canaux. Voici un exemple simple :

```go
func main() {
    // TELEGRAM
     chats, err := tel.HelperGetChatIds()
     if err != nil {
      fmt.Println(err)
     }

     chatid := chats["myUsername"]
     if chatid == 0 {
      fmt.Println("ChatId non trouvé")
     }

      // Initialiser le notificateur Telegram avec votre ChatID et token
     tel := notifyme.Telegram(chatid, "telegram_token")

     notifiers := notifyme.Notifiers{tel}

     errs := notifiers.Notify("Mon titre", "bonjour le monde ! Ceci est mon message de notification")
     if errs != nil {
      fmt.Println(errs)
     }

     fmt.Println("Notification envoyée avec succès !")

     // Initialiser le notificateur Email
     email := notifyme.Email("fromEmail@gmail.com", "password", "toEmail@gmail.com", "smtp.gmail.com", "587")
     err = email.Notify("Mon titre", "Bonjour de NOTIFYme !")
     if err != nil {
      fmt.Println("Erreur lors de l'envoi de l'e-mail :", err)
     }

     // Initialiser le notificateur ntfy
     ntfy := notifyme.Ntfy("http://localhost:8080", "topic")
     _ = ntfy.Notify("Mon titre", "Bonjour de NOTIFYme !")
}
```
