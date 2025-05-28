# Output dei modelli



### Descrizione del Prompt `generate_prompt`

La funzione `generate_prompt` costruisce un prompt testuale per un modello di linguaggio naturale (LLM) con l'obiettivo di supportare la creazione di mostre museali tematiche.

## Scopo

Il prompt invita il modello a interpretare il ruolo di un curatore museale esperto di storia dell'arte, incaricato di organizzare una mostra basata su un tema iconografico specifico.

## Input

- `sample['input']`: il tema iconografico in forma testuale.  
- `sample['icon_code_class']`: il codice Iconclass associato al tema (standard internazionale di classificazione iconografica).  
- `sample['new_context']`: lista di opere d'arte candidate, con ID e descrizione.

## Output atteso

Una descrizione dettagliata di una mostra tematica, con selezione e giustificazione delle opere più adatte al tema.

---

## Codice del Prompt

```python
def generate_prompt(sample):
    prompt = f"""Sei un curatore museale esperto di storia dell'arte. Devi organizzare una piccola mostra tematica partendo da un tema iconografico e un insieme di opere d'arte.

    Tema iconografico: {sample['input']} (Codice Iconclass: {sample['icon_code_class']})

    Opere disponibili:
    """
    for i, item in enumerate(sample['new_context']):
        prompt += f"{i+1}. ID: {item['id']}, Descrizione: {item['description']}\n"

    prompt += "\nCrea una mostra descrivendo la selezione delle opere più adatte al tema, giustificando brevemente le scelte.<|im_end|>"
    return prompt
