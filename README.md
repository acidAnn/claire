# :bulb: claire
CLAIRE dataset (Clarifying Insertions from Revision Edits) for SemEval-2022 Task 7

## Creation Context
This dataset was originally created for SemEval-2022 Task 7: Identifying Plausible Clarifications of Implicit and Underspecified Phrases in Instructional Texts.
The organizers of this task were Michael Roth, Talita Anthonio and Anna Sauer at the [Institute for Natural Language Processing, University Stuttgart](https://www.ims.uni-stuttgart.de/).
For details on the task, see [the task website](https://clarificationtask.github.io) and [the CodaLab page](https://competitions.codalab.org/competitions/35210).

## Data
The dataset contains instructional texts from [wikiHow](https://www.wikihow.com), a platform for collaboratively edited how-to guides for everyday scenarios.
Each wikiHow article has a revision history that records the changes applied by different collaborators.

Each instance in CLAIRE is a sentence from a wikiHow article and five different revisions that insert a word or phrase. These revisions can serve as potential clarifications for information that was previously implicit or unclear in the text. 

The clarifications belong to one of four different types:
* Insertion of implicit references (IMPLICIT REFERENCE):
	* In the original version of a sentence, there was an implicit reference to a previously mentioned entity. The revision makes this reference explicit.
        * Example: "Visit the salon's website. Call and ask questions." -> "Call *the salon* and ask questions."
* Resolution of fused head noun phrases (FUSED HEAD):
	* In the original version, there is a noun phrase where the head noun is missing. The revision adds that noun.
	* Example: "The container must be exactly the same as the container you used to collect the water." -> "The container must be exactly the same *diameter* as the container you used to collect the water."
* Completion of noun compounds (ADDED COMPOUND):
   	* The revision adds a compound modifier to a noun to make its meaning more specific.
        * Example: "Send a card." -> "Send a *reminder* card."
* Resolution of metonymic relations (METONYMIC REFERENCE):
        * In the original version, a noun is used in a metonymy. The revision makes the particular component or aspect of a noun explicit that is meant.
        * Example: "Screw each stringer to the deck frame with a drill." -> "Screw each stringer to *the top of* the deck frame with a drill."

## Annotations
Each clarification is annotated with information how plausible it is in the given context.
These annotations are released in two different forms:
* For a ranking task: an score on a continuous scale from 1 (very implausible) to 5 (very plausible)
* For a classification task: one of three discrete class labels IMPLAUSIBLE, NEUTRAL or PLAUSIBLE

## Data Format
For every data split (train, dev, test), there are three seperate TSV files:
* `{split}_data.tsv`: contains the instances themselves without annotation
* `{split}_scores.tsv`: contains the annotations as continuous plausibility scores between 1 and 5
* `{split}_labels.tsv`: contains the annoations as discrete plausiblity classes

`{split}_data.tsv` contains the following columns:
* "Id": an integer identifier
* "Resolved pattern": name of the clarification phenomenon (cf. list above: IMPLICIT REFERENCE, FUSED HEAD, ADDED NOUN, METONYMIC REFERENCE)
* "Article title": title of the wikiHow article in which the sentence occurs
* "Section header": heading of the section which the sentence is part of
* "Previous context": a couple of sentences that occur before the sentence in question - omissions are marked by "(...)"
* "Sentence": the sentence with a placeholder "______" that marks where the fillers should be inserted
* "Follow-up context": a couple of sentences that occur after the sentence in question - omissions are marked by "(...)"
* "Filler1" to "Filler5": the five different fillers

`{split}_scores.tsv` contains the following columns:
* The identifier, a string that consists of three parts:
	* it starts with an integer representing the id of the instance
        * next, there is an underscore
        * finally, the id of the filler (1 to 5)
        * e. g. "42_1" stands for the sentence with id 42 with filler 1
* The plausibility score, a float between 1 and 5

        
`{split}_labels.tsv` contains the following columns:
* The identifier string
* The class label that is IMPLAUSIBLE, NEUTRAL or PLAUSIBLE
 
## License
Since wikiHow articles are released under a [Attribution-NonCommerical-Share Alike 3.0 Creative Commons License (CC BY-NC-SA 3.0)](https://creativecommons.org/licenses/by-nc-sa/3.0/") (see [wikiHow](https://www.wikihow.com/wikiHow:Creative-Commons) for more information), CLAIRE is also made available under CC BY-NC-SA 3.0.
