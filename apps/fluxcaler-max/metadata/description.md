# Fluxcaler Max (Max VPS)

Max, l'assistant de code IA, **hébergé sur votre propre serveur** : il lit et
écrit votre code, exécute vos tâches et pilote vos projets, sans rien installer
sur votre poste. Vos données de travail restent chez vous (souveraineté ZDR).

- Accès : `https://max-ops-<votre-instance>.fluxcaler.net` (identifiant `opencode`)
- Inférence : vos crédits Fluxcaler via l'AI-Proxy (la clé est injectée à
  l'installation, jamais embarquée dans l'image)
- Canal : **stable uniquement** (`registry.fluxcaler.net/fluxcaler/max:X.Y.Z`)

## ⚠️ Installation vs mises à jour

- **Installation initiale** : réalisée par l'équipe Fluxcaler (orchestrateur
  Central : conteneur + route tunnel + DNS + identifiants + carte espace
  membre). La tuile seule ne configure PAS l'accès public.
- **Mises à jour** : à chaque release stable, cette tuile affiche « Mise à jour
  disponible » pour les instances installées via Runtipi. Les instances posées
  par l'orchestrateur sont mises à jour par la boucle orchestrée Fluxcaler
  (`max-vps-update.sh`, progressive staging → flotte).
