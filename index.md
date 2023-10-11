


{:.no_toc}
* toc
{:toc}
# DASpeech: Directed Acyclic Transformer for Fast and High-quality Speech-to-Speech Translation

Direct speech-to-speech translation (S2ST) translates speech from one language into another using a single model. However, due to the presence of linguistic and acoustic diversity, the target speech follows a complex multimodal distribution, posing challenges to achieving both high-quality translations and fast decoding speeds for S2ST models. In this paper, we propose DASpeech, a non-autoregressive direct S2ST model which realizes both fast and high-quality S2ST. To better capture the complex distribution of the target speech, DASpeech adopts the two-pass architecture to decompose the generation process into two steps, where a linguistic decoder first generates the target text, and an acoustic decoder then generates the target speech based on the hidden states of the linguistic decoder. Specifically, we use the decoder of DA-Transformer as the linguistic decoder, and use FastSpeech 2 as the acoustic decoder. DA-Transformer models translations with a directed acyclic graph (DAG). To consider all potential paths in the DAG during training, we calculate the expected hidden states for each target token via dynamic programming, and feed them into the acoustic decoder to predict the target mel-spectrogram. During inference, we select the most probable path and take hidden states on that path as input to the acoustic decoder. Experiments on the CVSS benchmark demonstrate that DASpeech can achieve comparable or even better performance than the state-of-the-art S2ST model Translatotron 2, while preserving up to 18.53× speedup compared to the autoregressive baseline model. Compared with the previous non-autoregressive S2ST model, DASpeech does not rely on knowledge distillation and iterative decoding, achieving significant improvements in both translation quality and decoding speed. Furthermore, DASpeech shows the ability to preserve the speaker's voice of the source speech during translation.

Audio samples are available at <a href="https://ictnlp.github.io/daspeech.github.io/"><i>https://ictnlp.github.io/daspeech.github.io/</i></a>.

<br>



# Translation Results

DASpeech: Our model with joint-viterbi decoding (λ=0.5) .

Translatotron: Baseline model in `Direct speech-to-speech translation with a sequence-to-sequence model` .

Translatotron 2: Baseline model in `Translatotron 2: High-quality direct speech-to-speech translation with voice preservation` .

S2UT: Baseline model in `Direct Speech-to-Speech Translation With Discrete Units` .

UnitY: Baseline model in `UnitY: Two-pass Direct Speech-to-speech Translation with Discrete Units` .

TranSpeech: Baseline model in `TranSpeech: Speech-to-Speech Translation With Bilateral Perturbation`.

<br>



## CVSS-C Fr-En

S2ST results on CVSS-C Fr→En test sets. "Sample id" denotes the id of the source audio. "ASR" denotes the speech recognition result of the corresponding audio.

<table>
    <tr>
        <th colspan="1" style="text-align: center">Sample id</th>
        <th colspan="2" style="text-align: center">Ground truth</th>
        <th colspan="4" style="text-align: center">Predictions</th>
    </tr>
    <!-- 1 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_17960551 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/source/10.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/ground_truth/10_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/daspeech/10_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron/10_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron2/10_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> no it is only an interruption </td>
        <td style="text-align: center"> no that's ays an interruption </td>
        <td style="text-align: center"> no this is just an interruption </td>
    </tr>
    <tr>
        <td style="text-align: center"> Non, ce n’est qu’une interruption… </td>
        <td style="text-align: center"> no it's only an interruption </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/s2ut/10_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/unity/10_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/transpeech/7012_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> no this is an interection </td>
        <td style="text-align: center"> no this is only an interruption </td>
        <td style="text-align: center"> this is what is interruption </td>
    </tr>
    <!-- 2 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_19601543 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/source/3829.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/ground_truth/3829_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/daspeech/3829_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron/3829_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron2/3829_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> it indicates the value of the slope </td>
        <td style="text-align: center"> he indicates the valley of the ten </td>
        <td style="text-align: center"> he indicates the value of the weight </td>
    </tr>
    <tr>
        <td style="text-align: center"> Il indique la valeur de la pente. </td>
        <td style="text-align: center"> it indicates the value of the slope </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/s2ut/3829_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/unity/3829_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/transpeech/8713_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> he indicates the value of the store </td>
        <td style="text-align: center"> he shows the value of the door </td>
        <td style="text-align: center"> he indicates the slow value </td>
    </tr>
    <!-- 3 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_17740817 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/source/8194.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/ground_truth/8194_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/daspeech/8194_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron/8194_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/translatotron2/8194_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> since it wasn't raining we didn't go to the movies </td>
        <td style="text-align: center"> since it was not crane we did not go to the movies </td>
        <td style="text-align: center"> since he was not raining we didn't go to the cinema </td>
    </tr>
    <tr>
        <td style="text-align: center"> Puisqu’il ne pleuvait pas nous n’étions pas allés au cinéma. </td>
        <td style="text-align: center"> since it wasn't raining we didn't go to the movies </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/s2ut/8194_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/unity/8194_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo/transpeech/12959_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> since it was not raining we didn't go to the cinema </td>
        <td style="text-align: center"> since it was not raining it didn't go to the movies </td>
        <td style="text-align: center"> since it wasn't raining we won't go to the movies </td>
    </tr>
</table>

<br>



## CVSS-T Fr-En

S2ST results on CVSS-T Fr→En test sets.

<table>
    <tr>
        <th colspan="1" style="text-align: center">Sample id</th>
        <th colspan="2" style="text-align: center">Ground truth</th>
        <th colspan="4" style="text-align: center">Predictions</th>
    </tr>
    <!-- 1 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_17960551 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/source/10.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/ground_truth/10_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/daspeech/10_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron/10_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron2/10_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> no it is only an interruption </td>
        <td style="text-align: center"> no it is a indirection </td>
        <td style="text-align: center"> no this is only one interruption </td>
    </tr>
    <tr>
        <td style="text-align: center"> Non, ce n’est qu’une interruption… </td>
        <td style="text-align: center"> no it's only an interruption </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/s2ut/10_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/unity/10_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/transpeech/7012_pred.wav"                           type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> no it is only a stranger </td>
        <td style="text-align: center"> no this is only one interruption </td>
        <td style="text-align: center"> so this is interruption </td>
    </tr>
    <!-- 2 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_19601543 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/source/3829.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/ground_truth/3829_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/daspeech/3829_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron/3829_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron2/3829_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> it indicates the value of the slope </td>
        <td style="text-align: center"> i gosis value of io </td>
        <td style="text-align: center"> it indicates the value of the door </td>
    </tr>
    <tr>
        <td style="text-align: center"> Il indique la valeur de la pente. </td>
        <td style="text-align: center"> it indicates the value of the slope </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/s2ut/3829_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/unity/3829_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/transpeech/8713_pred.wav"                           type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> he indicates the value of the punt </td>
        <td style="text-align: center"> he indicates the value of the pont </td>
        <td style="text-align: center"> he indicates the value of the scup </td>
    </tr>
    <!-- 3 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>fr_17740817 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/source/8194.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/ground_truth/8194_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/daspeech/8194_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron/8194_pred.wav"  type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/translatotron2/8194_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> since it wasn't raining we didn't want to the movies </td>
        <td style="text-align: center"> since this was not rain hande ito </td>
        <td style="text-align: center"> since it was not raining we didn't go to the movies </td>
    </tr>
    <tr>
        <td style="text-align: center"> Puisqu’il ne pleuvait pas nous n’étions pas allés au cinéma. </td>
        <td style="text-align: center"> since it wasn't raining we didn't go to the movies </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
        <th style="text-align: center">TranSpeech</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/s2ut/8194_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/unity/8194_pred.wav"          type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_t/transpeech/12959_pred.wav"                           type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> since it wasn't raining we did not go to the movies </td>
        <td style="text-align: center"> since it was not raining we didn't go to the movies </td>
        <td style="text-align: center"> since it war not raining we won't go to the movies </td>
    </tr>
</table>

<br>



## CVSS-C X-En

Multilingual X→En S2ST results on CVSS-V test sets. "De" denotes Germany. "Es" denotes Spanish. "It" denotes Italian.

<table>
    <tr>
        <th colspan="1" style="text-align: center">Sample id</th>
        <th colspan="2" style="text-align: center">Ground truth</th>
        <th colspan="3" style="text-align: center">Predictions</th>
    </tr>
    <!-- 1 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>de_19650355 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/source/common_voice_de_19650355.mp3"       type="audio/mp3"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/ground_truth/common_voice_de_19650355.mp3.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/daspeech/18227_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/translatotron2/18227_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> originally he wanted to become a journalist </td>
        <td style="text-align: center"> initially he wanted to be a journalist </td>
    </tr>
    <tr>
        <td style="text-align: center"> Ursprünglich wollte er Journalist werden. </td>
        <td style="text-align: center"> originally he wanted to be a journalist </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/s2ut/18227_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/unity/18227_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> originally he wanted to take a list </td>
        <td style="text-align: center"> initially he wanted to be a journalist </td>
    </tr>
    <!-- 2 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>es_19723874 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/source/common_voice_es_19723874.mp3"       type="audio/mp3"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/ground_truth/common_voice_es_19723874.mp3.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/daspeech/29025_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/translatotron2/29025_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> his grandmother was born in ireland </td>
        <td style="text-align: center"> his grandfather was born in ireland </td>
    </tr>
    <tr>
        <td style="text-align: center"> Su abuela nació en Irlanda. </td>
        <td style="text-align: center"> his grandmother was born in ireland </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/s2ut/29025_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/unity/29025_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> his wife is born in ireland </td>
        <td style="text-align: center"> his wile was native to ireland </td>
    </tr>
    <!-- 3 -->
    <tr>
        <th rowspan="6" style="text-align: center"> common_voice_<br>it_20047586 </th>
        <th style="text-align: center">Source audio</th>
        <th style="text-align: center">Target audio</th>
        <th> Model </th>
        <th style="text-align: center">DASpeech</th>
        <th style="text-align: center">Translatotron 2</th>
    </tr>
    <tr>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/source/common_voice_it_20047586.mp3"       type="audio/mp3"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/ground_truth/common_voice_it_20047586.mp3.wav"       type="audio/wav"></audio></center>
        </th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/daspeech/61159_pred.wav"       type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/translatotron2/61159_pred.wav" type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th style="text-align: center">Source text</th>
        <th style="text-align: center">Target text</th>
        <th> ASR </th>
        <td style="text-align: center"> the initial staff exceeded ten thousand units </td>
        <td style="text-align: center"> the initial staff exceeded ten thousand units </td>
    </tr>
    <tr>
        <td style="text-align: center"> Lo staff iniziale superava le diecimila unità. </td>
        <td style="text-align: center"> the initial staff exceeded the ten thousand units </td>
        <th> Model </th>
        <th style="text-align: center">S2UT</th>
        <th style="text-align: center">UnitY</th>
    </tr>
    <tr>
        <th rowspan="2" colspan="2"></th>
        <th> Audio </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/s2ut/61159_pred.wav"           type="audio/wav"></audio></center>
        </th>
        <th>
            <center><audio controls style="width: 140px;"><source src="wav_for_demo_x/unity/61159_pred.wav"          type="audio/wav"></audio></center>
        </th>
    </tr>
    <tr>
        <th> ASR </th>
        <td style="text-align: center"> the initial station was about ten million units </td>
        <td style="text-align: center"> the initial state was exceeding ten thousand units </td>
    </tr>
</table>



