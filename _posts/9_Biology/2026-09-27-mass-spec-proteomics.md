---
layout: post
title: Mass spectrometry proteomics data
status: ongoing
categories: biology
author: exma23
---
# **Overview**
Shotgun proteomics is a strategy for broad proteome analysis without pre-selecting specific proteins. Bottom-up proteomics is a specific type of shotgun - sample preparation involving the conversion of proteins into peptides via proteases, followed by LC-MS/MS analysis.

LC-MS generates two different types of plots that are easily confused:
- Chromatogram (TIC or EIC): the x-axis represents retention time, and the y-axis represents intensity. Each peak corresponds to a substance (or a specific ion) eluting from the column at that time.
- Mass spectrum: the x-axis represents m/z, and the y-axis represents intensity. This spectrum is acquired at a specific point in time (or for a specific chromatographic peak).

The workflow starts with **sample preparation**. Cells or tissues are lysed and proteins are extracted. Disulfide bonds are reduced and alkylated, after which proteins are digested with **trypsin**, which typically cuts after lysine (K) and arginine (R), producing peptides. The sample is then cleaned to remove salts and other interfering substances.

Because the resulting peptide mixture can contain tens of thousands of different peptides, the peptides are first separated by **liquid chromatography (LC)**. In a typical reversed-phase C18 column, peptides elute at different **retention times (RTs)** depending on their interactions with the column. The separated peptides then enter the mass spectrometer.

The mass spectrometer first ionizes the peptides, commonly using **electrospray ionization (ESI)**, producing charged peptide ions such as \([M+2H]^{2+}\) or \([M+3H]^{3+}\). The instrument then alternates between **MS1** and **MS2** measurements. MS1 measures the \(m/z\) values of peptide ions currently entering the instrument, while MS2 selects peptide ions called **precursors**, fragments them, and measures the \(m/z\) values of the resulting fragment ions.

The raw LC-MS data can be viewed as a three-dimensional signal containing **retention time, \(m/z\), and intensity**. An LC chromatogram plots RT against intensity; a **TIC** sums the signal from all ions, while an **XIC** extracts the signal for a particular \(m/z\) value. The area under an XIC peak is commonly used as a measure of peptide abundance. An MS1 spectrum instead plots \(m/z\) against intensity at a particular RT, showing which peptide ions are present and their mass-to-charge ratios. An MS2 spectrum plots the \(m/z\) and intensity of fragment ions produced from one precursor. Fragment-ion patterns, particularly the \(b\)- and \(y\)-ion series, provide information about the peptide sequence.

For **peptide identification**, software such as MaxQuant, Proteome Discoverer, or MSFragger compares experimental MS2 spectra with theoretical spectra generated from a protein database after in-silico tryptic digestion. Candidate peptide-spectrum matches (PSMs) are scored and filtered using a target-decoy strategy to control the false discovery rate (FDR), commonly at 1%. Identified peptides can then be mapped back to proteins.

For **quantification**, label-free methods typically use MS1 XIC peak areas to estimate peptide abundance across samples, followed by normalization and comparison between samples. A simpler alternative is spectral counting, which counts the number of MS2 spectra assigned to a protein. In isobaric labeling methods such as TMT or iTRAQ, different samples receive different labels and are analyzed together; reporter-ion intensities in MS2 provide relative abundance information for each sample. In **DIA**, instead of selecting individual precursor ions, the instrument fragments all ions within predefined \(m/z\) windows, and the resulting MS2 fragment signals are used for peptide identification and quantification.

In LC-MS, one MS1 spectrum is a snapshot of many peptides present at the same retention time (RT), so one peptide is typically observed across many consecutive MS1 spectra as it elutes from the column; these repeated measurements form its XIC over RT. MS2 is closer to a one-to-one relationship, because each MS2 scan typically isolates and fragments one selected peptide precursor to produce one MS2 spectrum, although the relationship is not always perfectly one-to-one.

# **0. Chromatography**
Liquid chromatography (LC) is a separation technique used to separate a mixture of peptides before they enter the mass spectrometer. The peptide mixture is carried by a liquid mobile phase through a chromatography column containing a stationary phase.

Different peptides interact differently with the column material. Peptides with weaker interactions travel through the column faster, while peptides with stronger interactions are retained longer. The time required for a peptide to pass through the column and reach the mass spectrometer is called the retention time (RT). LC converts a complex peptide mixture into a time-separated signal. The mass spectrometer then measures the \(m/z\) values of peptides as they elute at each retention time. In LC-MS, peptide identification uses both pieces of information.

LC uses an enzyme called trypsin. Trypsin cleaves a protein sequence **after lysine (K) or arginine (R)**, except when K/R is followed by proline (P), which prevents cleavage. Therefore, the number of cleavage sites depends on the number and positions of K/R residues in the protein sequence, and a protein typically produces **dozens of peptides** of different lengths. In ideal digestion, each cleavage creates a new peptide boundary, so the number of resulting peptides is approximately the number of effective cleavage sites plus one. In practice, trypsin may fail to cleave some K/R sites, known as **missed cleavages**, producing longer peptides than expected; proteomics software explicitly accounts for these possibilities during peptide identification.

# **1. Stage 1: distinguish data TMT - Label free - SILAC**
- SILAC is a labeling technique in wet lab, cell lysis—cells are cultured in media containing "heavy" amino acids (e.g., Lys8, Arg10), meaning the label is incorporated into the proteins/peptides from the very beginning.During MS analysis: two peptides with the same sequence (light vs. heavy) possess different masses, appearing as two distinct peaks separated by a fixed Δm/z value in the MS1 spectrum. The intensity ratio between that pair represents the protein expression ratio between the two conditions (two SILAC labels), this is a method for relative quantification that does not require running two separate samples. This ratio is calculated directly from the MS1 data, while MS2 is used solely for sequence identification.
    - Isotope cluster detection is identifying a peptide based on its natural isotope pattern (C12/C13, etc.) in the (m/z, RT, intensity) space. While both are labeling techniques used for quantification, they differ significantly in their mechanisms and the specific stage of the MS pipeline where detection occurs - a crucial distinction that dictates the use of completely different data processing algorithms.
    - However, the number of samples that can be multiplexed is low (typically 2–3, due to label constraints), and MS1 spectral complexity increases (resulting in more overlapping peaks).

- TMT (Tandem Mass Tag) is a chemical/isobaric labeling which is detected at the MS2 level. The label is chemically attached after protein digestion into peptides (unlike metabolic labeling, which occurs within the living cell). TMT tags share the same total mass (isobaric) regardless of the sample they label; consequently, peptides with identical sequences from different samples appear identical in the MS1 spectrum, manifesting as a single peak (unlike the separation seen in SILAC).
    - Only upon fragmentation (MS2/MS3) do the tags cleave to release reporter ions with distinct masses specific to each sample (e.g., 126, 127, 128 Da); the intensities of these reporter ions are then measured to determine the quantification ratios. Advantages: significantly higher sample multiplexing capacity (6-, 10-, 16-, 18-plex, etc.) and a simpler MS1 spectrum (fewer overlapping peaks).
    - TMT tags within the same set have the same total mass (isobaric) and essentially the same chemical structure; they differ in the distribution of heavy isotopes within the tag.
    - On Thermo Fisher, TMT 11-plex can be up to 11 samples per run. While in, TMTpro 35-plex, it is up to 35 samples per run.

# **2. Stage 2: MS1**
- Official documentation: Thermo Fisher – Overview of Mass Spectrometry
peak, isotope cluster
- How to calculate: In a time-of-flight (TOF) mass spectrometer, ions are first accelerated by an electric field. The charge of an ion is given by \(q = ze\), where \(z\) is the charge state and \(e\) is the elementary charge. When a potential difference \(V\) is applied, the electrical energy is converted into kinetic energy:
        \[ qV = \frac{1}{2}mv^2 \]
    Therefore, the velocity of the ion is:
        \[ v = \sqrt{\frac{2qV}{m}} \]
    By substituting \(q = ze\), we obtain:
        \[ v = \sqrt{\frac{2zeV}{m}} \]
    After acceleration, the ion travels through a flight tube with length \(L\). The time required for the ion to reach the detector is:
        \[ t = \frac{L}{v} \]
    Substituting the velocity equation gives:
        \[ t = L\sqrt{\frac{m}{2zeV}} \]
    Since \(L\), \(V\), and \(e\) are constants in the instrument, the flight time depends on the mass-to-charge ratio:
        \[ t \propto \sqrt{\frac{m}{z}} \]
    or equivalently: \[ \frac{m}{z} \propto t^2 \]
Therefore, by measuring the flight time \(t\), the TOF mass spectrometer can determine the mass-to-charge ratio (\(m/z\)) of each ion. This time-of-flight measurement is the fundamental physical principle behind TOF mass spectrometry.

- In LC-MS, the mass spectrum alone is not sufficient because many peptides can have similar mass-to-charge ratios (`m/z`). Therefore, LC-MS combines information from both the chromatogram and the mass spectrum. The raw LC-MS data can be represented as a three-dimensional signal:
\[
(\text{retention time},\ m/z,\ \text{intensity})
\]
The liquid chromatography (LC) step separates peptides based on their retention time (RT). For example, peptide A may elute at RT = 8.2 minutes, while peptide B may elute at RT = 10.5 minutes. At a specific retention time, the mass spectrometer measures the mass spectrum of the ions present at that moment. For example, at RT = 8.2 minutes, the mass spectrum may contain peaks at different mass-to-charge ratios:
\[
m/z = 523.3,\ 650.2,\ldots
\]
By combining the retention time information from LC and the mass-to-charge ratio information from MS, we can identify a peptide:
\[
\text{RT} \approx 8.2\ \text{min} + m/z = 523.3
\]
corresponds to a specific peptide candidate. After identifying a peptide ion with a specific \(m/z\), we can extract its extracted ion chromatogram (XIC): \[ \mathrm{XIC}_{523.3}(t) \]
which represents the intensity of this ion over time. The area under the XIC peak is calculated as: \[ A = \int I(t)\,dt \]. where \(I(t)\) is the ion intensity at time \(t\). This peak area represents the peptide signal intensity and is commonly used for peptide quantification in proteomics.

- In mass spectrometry graph, a peak is a signal detected at a specific mass-to-charge ratio (\(m/z\)), representing an ion (or a group of isotopic ions) present in the sample. In a mass spectrum, the x-axis represents the \(m/z\) value, which indicates the mass-to-charge ratio of detected ions, while the y-axis represents the signal intensity, indicating the relative abundance of ions at each \(m/z\) value. A higher peak means that more ions with that specific \(m/z\) were detected.

Different types of peaks provide different information. The base peak is the most intense peak in the spectrum and is normalized to 100% intensity. Molecular ion peaks represent intact ionized molecules and provide information about molecular mass, while fragment peaks are produced when molecules break into smaller ions and are used for structural identification. Isotope peaks (such as M+1 or M+2) arise from naturally occurring isotopes and can provide information about elemental composition.

For example, a peak at \(m/z = 180\) with the highest intensity indicates that an ion with this mass-to-charge ratio is the most abundant ion detected in the spectrum (assuming \(z=1\)).
# **3. Stage 3: MS2 (DIA - DDA)**
- Official documentation:
    - Thermo Fisher - Orbitrap precursor isolation manual.
    - Thermo Fisher - Proteomics acquisition example.
    - Thermo Fisher - DIA proteomics example.

- MS1 indicates "how many precursor ions are present and their intensities," while MS2 reveals "which ions the precursor fragments into" thereby enabling peptide identification with higher specificity. Both MS1 and MS2 can be used for quantification, depending on the acquisition or quantification strategy.
    - The difference between each mass will be used to calculate/predict the string.

- DDA and DIA can be understood as two different **MS2 acquisition strategies**. In both approaches, MS1 measures the peptide ions present at each moment; the main difference is how the instrument decides which ions to fragment. In **DDA (Data-Dependent Acquisition)**, the instrument looks at the MS1 spectrum and selects the strongest individual peptide ions (typically the top N) for isolation and fragmentation. As a result, each MS2 spectrum is relatively clean and usually corresponds to one precursor peptide. In **DIA (Data-Independent Acquisition)**, the instrument does not select individual peptides. Instead, it divides the \(m/z\) range into relatively wide windows and fragments all peptide ions within each window simultaneously, producing mixed MS2 spectra containing fragments from multiple peptides.

Because DDA produces cleaner MS2 spectra, peptide identification can be relatively straightforward, but weaker peptides may be missed and the same peptides may not be selected consistently across runs, leading to more missing values. DIA provides more systematic and reproducible sampling because the same \(m/z\) windows are repeatedly measured across the run, reducing missing values. However, its MS2 spectra are more complex because fragments from multiple peptides are mixed together, so identification and quantification require computational methods to disentangle the mixed signals, often using spectral libraries or library-free approaches.

- DDA:
    - Why only selecting a few peptides: Peptides generate a strong signal only for a limited period.
- DIA (data-independent acquisition): The instrument divides peptides spectra into windows. A window is an m/z range selected by the instrument to allow ions to proceed to the MS2 stage. Specifically, the quadrupole uses this window to filter precursor ions based on their m/z. All precursors within a single window are fragmented together, rather than selecting individual precursors based on intensity as in DDA.

# **4. Stage 4: mapping peptide to proteins**
- Official documentation: Thermo Fisher - Proteome Discoverer User Guide

- ProteinProphet: calculate the overall probability that a specific protein is present in a sample based on the collective probability of the individual peptides assigned to it from tandem mass spectrometry (MS/MS) data.

MS1 provides **precursor peptide abundance over time**, typically quantified from the MS1 XIC or peak area. MS1 + MS2 DDA provides **peptide abundance and fragmentation patterns**, which are used for peptide identification and sequencing. MS1 + MS2 DIA provides **peptide abundance from precursor and/or fragment signals**, together with fragmentation information for peptide identification.


- After peptide identification, protein inference faces the problem of assigning identified peptides to protein groups. Each protein group \(G_i\) is associated with an evidence set \(E_{G_i}\), which contains the peptides that can be explained by that group. However, some peptides are shared between multiple protein groups because different proteins may contain the same sequence region (for example, homologous proteins or isoforms). These shared peptides create ambiguity: a peptide such as \(p_3\) may provide evidence for both \(G_1\) and \(G_2\), so we need to decide which protein group should receive the quantification credit:

    A common strategy is the **razor peptide approach**, based on a greedy version of the **Occam's razor principle**. The algorithm starts with all unidentified peptides in a set called `Pep_remaining`. At each iteration, it selects the protein group that explains the largest number of currently remaining peptides:

        \[ G^* = \arg\max_G |E_G \cap \text{Pep}_{remaining}| \]

    The selected group receives all peptides that it can uniquely explain at that point, including shared peptides. These assigned peptides are then removed from `Pep_remaining`, and the process continues until all peptides are assigned.

    For example, if \(G_1\) explains \(\{p_1,p_2,p_3\}\), \(G_2\) explains \(\{p_3,p_4\}\), and \(G_3\) explains \(\{p_5\}\), then \(G_1\) is selected first because it explains the largest number of peptides. Therefore, the shared peptide \(p_3\) is assigned as a razor peptide to \(G_1\), while \(G_2\) only receives \(p_4\) in the next iteration. The final assignment becomes: \(G_1: \{p_1,p_2,p_3\}\), \(G_2: \{p_4\}\), and \(G_3: \{p_5\}\).

    This method is related to the **minimum set cover problem** in computer science. In set cover, the goal is to select the smallest number of sets that cover all elements. Here, the universe is the set of identified peptides, and each protein group represents a set of peptides. Since exact set cover is NP-hard, practical protein inference algorithms use greedy approximation methods: at each step, they choose the protein group that covers the largest number of currently unexplained peptides. The additional step in protein inference is that peptides must not only be covered but also assigned to a specific protein group for downstream quantification, which motivates the concept of razor peptides.

- Beside, there is also correction stuff such as PEP. The core idea of PEP estimation is to use target-decoy score distributions to estimate the probability that each peptide-spectrum match (PSM) is incorrect, assigning a confidence value to individual PSMs instead of relying on a single arbitrary score cutoff.
# **5. Summary**

In a typical DDA LC-MS run, the number of MS1 spectra is approximately the number of acquisition cycles. For a 90-minute run with a cycle time of 1–3 seconds, this corresponds to roughly **1,500–5,000 MS1 spectra**. Each cycle can then select multiple peptides for fragmentation (e.g. Top 10–40), so the number of MS2 spectra can be roughly an order of magnitude larger. For example, 3,000 cycles with Top 15 would produce about **3,000 MS1 spectra and 45,000 MS2 spectra**. These are rough estimates because the actual numbers depend on the instrument, sample complexity, and acquisition settings.

Each MS2 spectrum also retains information about **which peptide was selected from MS1**, including its precursor m/z, charge, retention time, and scan information linking it to the acquisition event. Conceptually, an MS2 spectrum means: **“this peptide signal was selected from MS1, and these are the fragment signals produced from it.”** This link allows software to connect the peptide signal observed in MS1 with the fragment pattern observed in MS2 for peptide identification.

During MS2, a peptide is not simply cut into a few fixed-length pieces. Instead, fragmentation can occur at many positions along the peptide backbone, producing fragments of different lengths. For a peptide of length \(n\), there are \(n-1\) possible cleavage positions, and the resulting fragments are commonly represented as **b-ions** from the N-terminus and **y-ions** from the C-terminus. Thus, a single MS2 spectrum can contain fragments ranging from very short sequences to fragments almost as long as the original peptide, with different intensities depending on the fragmentation process.
