1) Placer les deux fichiers .ser sur le bureau

information utilisateur existant
=====================
ID : root
PW : root
=====================

* dans la conception, je partais du principe qu'un client peux avoir des sous dans son compte, donc pour le traitement de retrait, je garde uniquement le int.

* pour la data, elle se fait tout seul du a mon interface Utilitaire et il y a une simple serialisation lors que la cloturation.
* Aucune implémentation de PaimentFacture
* Il faut que le le client est obligatoirement un compte, sinon il sera bloquer dans le processus de connection
* Il peut y a voir un bug avec la serialisation, parfois, il ne sauvegarde pas les comptes de l'utilisateur, donc le compte deviens bloquer.
Il faut pour cela recrée des comptes. 

****BUG de connection problablement resolue (j'ai cru trouver mon erreur) sinon, si la serialization a des probleme ou que les id en haut ne marche pas,
remplaer Application.java par le code si dessous

package leo.cirpaci.guichet;

import javafx.event.EventHandler;
import javafx.fxml.FXMLLoader;
import javafx.scene.Scene;
import javafx.stage.Stage;
import javafx.stage.WindowEvent;
import ressource.Utilisateur;
import ressource.compte.Cheque;
import ressource.compte.Epargne;
import ressource.compte.Hypothecaire;
import ressource.system.Guichet;
import ressource.system.PackageData;
import ressource.system.Utilitaire;
import ressource.utilisateur.Administrateur;
import ressource.utilisateur.Client;

import java.io.IOException;

public class Application extends javafx.application.Application {
    @Override
    public void start(Stage stage) throws IOException {
        FXMLLoader fxmlLoader = new FXMLLoader(Application.class.getResource("Connexion.fxml"));
        Scene scene = new Scene(fxmlLoader.load(), 260, 280);
        stage.setTitle("Guichet");
        stage.setScene(scene);
        stage.setResizable(false) ;
        stage.show();
        Guichet.toogleOuvert();
        Administrateur admin = new Administrateur() ;
        admin.setMotDePasse("root");
        admin.setIdentifiant("root");
        Utilitaire.utilisateurs.add(admin) ;
    }
    public static void main(String[] args) {
        launch();
    }
}