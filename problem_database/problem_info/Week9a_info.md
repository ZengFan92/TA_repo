Week9a

Week9a Correct Answer data missing.


Assigned problem file name:

    +--------+------------+-----------------------------------------------+
    | set_id | problem_id | source_file                                   |
    +--------+------------+-----------------------------------------------+
    | Week9a |          1 | local/Reorganized/RandomizedAlgs/min_hash1.pg |
    | Week9a |          2 | local/Reorganized/RandomizedAlgs/min_hash2.pg |
    | Week9a |          3 | Reorganized/RandomizedAlgs/Hashing_6.pg       |
    +--------+------------+-----------------------------------------------+


Problem 1

    $A = random(1000,2000,1000);
    $B = random(600,900,100);
    $AB = random(100,300,100);
    $n = random(80,100,10);
    $m = random(700,1000,100);

    ## Min-Hash ##

    You can find the relevant material for this problem in section 11.6 of the lecture notes on Nota-Bene (http://nb.mit.edu)

    Suppose that the sets [`A,B,C,\ldots`] are subsets of the domain [`U=\{1,\ldots,n\}`] with [`n=[$n]`] and suppose that we have a family of hash functions [`h_1,h_2`], which map from [`U`] to the a much larger set [`\{1,\ldots,m\}`] with [`m=[$m]`].

    a) Fix some integers [`i,j`] such that [`1 \leq i \leq j \leq n`]. What is the
    probability that [`h_1(i)=h_1(j)`]? [_______________]{Compute("$n/$m")}

    b) Now suppose that [`m`] is much larger than [`n`], so that [`n/m`] is a
    negligibly small number. Recall that given a hash function [`h`] the Min-Hash of a set [`S`] is defined to be [`\min_{s \in S} h(s)`]. Suppose that we have two sets: [`A=\{1,2,3\}`] and [`B=\{3,0\}`]. What is the probability (over the random choice of the hash function) that
    [`MinHash(A)=MinHash(B)`]?    [________]{Compute("1./4")}

    Suppose the sets [`A,B`] are two subsets of the set [`S=\{1,2,\ldots,10000\}`]. Suppose  [`|A|=[$A]`], [`|B|=[$B]`], [`|A\cap B|=[$AB]`] are the sizes of [`A`], [`B`] and
    their intersections respectively. What is the probability that
    [`MinHash(A)=MinHash(B)`]?
    [________________________]{Compute("$AB/($A+$B-$AB)")}

    The ratio [`\frac{|A\cap B|}{|A\cup B|}`] is called the Jaccard similarity of
    [`A`] and [`B`].


Problem 2

    $k=random(3,5,1);

    ## Shingles ##

    Consider the sentence "there are no people like show people". If we
    consider the sentence as a set of words then it is a set of size
    [_________]{6} (Note that the word "people" appears twice).

    Note that representing a document as a set of words means that we are
    ignoring the meaning of the sentence. Clearly, the order of words in a
    sentence contain its meaning

    To capture some of the order information we can use
    "shingles". Shingles of length two are consecutive pairs of words. For
    the sentence above we get the 2-shingles: "there are", "are no", "no
    people", "people like", "like show", "show people".

    Suppose a document contains 1000 words, what is the maximal size of
    the set of [$k]-shingles that it defines?
    [__________]{"1000-($k-1)"}



Problem 3

    $a = Compute("0.05/sqrt(0.16/200)");
    $q = Compute("Q($a)");

    ## Detecting near-duplicates ##

    Near-duplication is pervasive in the web: there are large numbers of distinct URLs which have exactly
    the same content but differ only in unimportant details like headers and footers. The user of a search
    engine would not be pleased if the answer to his query was a set of 10 near-identical pages! In order
    to remove this redundancy, we need to define a notion of _similarity_ between documents.

    #### The similarity between two documents ####

    For any document---call it [`d`]---let the set of all words in [`d`] be denoted [`C(d)`]. For two documents
    [`d`] and [`d'`], we will measure their similarity by the function

    [$BCENTER]*
    [`` S(d,d') \ = \ \frac{|C(d) \cap C(d')|}{|C(d) \cup C(d')|} .``]
    [$ECENTER]*

    If the two documents are truly identical, [`S(d,d') = 1`]. If they are almost-identical, [`S(d,d')`] will
    be close to 1. And if they are completely different, with no words in common, then [`S(d,d')`] will be
    zero. We'll consider [`d`] and [`d'`] to be near-duplicates if [`S(d,d')`] is sufficiently close to 1.

    Now, imagine a search engine that is going through a list of documents or webpages, and wants to
    eliminate near-duplicates. Here's an algorithm it could use:

    * [`{\cal D} = \emptyset`] (set of documents, initially empty)
    * for each document [`d`] that appears:
        - if [`S(d,d')`] is significantly smaller than 1 for all [`d'`] in [`{\cal D}`]: add [`d`] to [`{\cal D}`]

    The final set of documents [`{\cal D}`] will contain no near-duplicates. This is good, but the
    algorithm is very slow. Suppose for the sake of simplicity that there are [`n`] documents in total,
    each of length [`L`]. Then computing the similarity between two documents takes [`O(L)`] time, and there are [________]{(n-1)n/2} pairs, thus the algorithm takes [`O(n^2L)`]. This quadratic dependence on [`n`] is prohibitive in web-scale applications,
    where [`n`] could easily be in the billions or tens of billions.

    To get a faster algorithm, we once again resort to hashing.

    ---

    Again for the example:

    A: [`\verb|Thanksgiving may be the perfect day to give thanks, but what about giving thanks to a delicious and flawless turkey?|`]

    B: [`\verb|Pick the perfect centerpiece for your Thanksgiving or holiday meal from our ultimate collection of roast turkey recipes.|`]



    After preprocessing, the document A is represented by the *set*  [`\{\verb|Thanksgiving, perfect, day, give, thanks, delicious, flawless, turkey|\}`], and

    document B becomes the *set* [`\{\verb|pick, perfect, centerpiece, Thanksgiving, holiday, meal, ultimate, collection, roast, turkey, recipe |\}`]


    The similarity between A and B is [__________]{"3/(8+11-3)"}.
