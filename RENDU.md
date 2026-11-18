# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   > 3 noeuds : 
      - 1 lab server : control-plane
      - 2 lab agents : aucune role attribué pour l'instant
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   > docker ps montre les container docker qui tourne sur la machine. Un noeud dans k3d correspond à une machine qui fournit des ressources pour tourner sur un cluster.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   > le deployment.apps web ainsi qu'une copie du pod ont été créés
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   > le status du pod "web" est passé en terminating et s'est supprimé dans le second terminal et l'accès à la page web n'est donc plus possible

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   > Non le message sur la page web n'a pas survécu car c'est le pod qui été en charge d'afficher la page web, en supprimant le pod la page n'est plus accessible
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   > Car le port-forward est défini pour exposer le port du pod, si on supprime le pod le tunnel définit est toujours attaché au pod mais comme il n'existe plus il se casse.

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   > create permet de créer un pod, un environnement, etc... et apply permet d'appliquer les configurations
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   > il permet de target le bon service qui doit recevoir le trafic

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   ```
   Chaque replica se trouve sur les noeuds existants : lab-server-0, lab-agent-0 et lab-agent-1
   kubectl get pods -l app=site -o wide
NAME                    READY   STATUS    RESTARTS   AGE     IP          NODE               NOMINATED NODE   READINESS GATES
site-6db5694449-gpccs   1/1     Running   0          52s     10.42.2.5   k3d-lab-server-0   <none>           <none>
site-6db5694449-np8vn   1/1     Running   0          3m59s   10.42.0.9   k3d-lab-agent-0    <none>           <none>
site-6db5694449-w799m   1/1     Running   0          52s     10.42.1.7   k3d-lab-agent-1    <none>           <none>
   ```
10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    > kubectl get pods -l app=site renvoit "ErrImagePull" puis "ImagePullBackOff"
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    > Non innaccessible car l'image sur laquelle il tournait était mauvaise donc impossible d'y accéder

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    > https://animated-barnacle-qrjx7q56494cxqxv-8585.app.github.dev/
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    > oui ils parlents aux même composant via kube-apiserver

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
