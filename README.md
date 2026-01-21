# Binary Transformer

Petit outil Python pour **transformer un fichier en binaire**, l'emballer avec un **décodeur** ajouté **à la fin du fichier**, puis le **déballer** facilement. Le paquet généré est autonome et contient:

- les données originales,
- un script de décodeur (attaché à la fin),
- un pied de page binaire (footer) avec les métadonnées.

## Utilisation

### Emballer un fichier

```bash
python3 binary_transformer.py pack ./mon_fichier.pdf
```

Résultat: `mon_fichier.pdf.btransformer`

### Déballer un fichier

```bash
python3 binary_transformer.py unpack ./mon_fichier.pdf.btransformer
```

Le fichier est extrait dans le dossier courant.

### Décodeur intégré

Le décodeur est embarqué à la fin du bundle. Vous pouvez le récupérer en lisant la fin du fichier et en utilisant la section `decoder` (voir le script généré pour un exemple).

## Format du bundle (résumé)

```
[DATA][DECODER][MAGIC][DECODER_LEN][DATA_LEN][FILENAME][FILENAME_LEN]
```

- `MAGIC` = `BTRANSFORMER1`
- longueurs en big-endian.

## Exemple rapide

```bash
python3 binary_transformer.py pack ./photo.jpg
python3 binary_transformer.py unpack ./photo.jpg.btransformer --output-dir ./sortie
```
