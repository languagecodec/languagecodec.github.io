{:.no_toc}

## Overview
<p align="justify">
In recent years, large language models have achieved significant success in generative tasks (e.g., speech cloning and audio generation) related to speech, audio, music, and other signal domains. A crucial element of these models is the discrete acoustic codecs, which serves as an intermediate representation replacing the mel-spectrogram. However, there exist several gaps between discrete codecs and downstream speech language models. Specifically, 1) most codec models are trained on only 1,000 hours of data, whereas most speech language models are trained on 60,000 hours; 2) Achieving good reconstruction performance requires the utilization of numerous codebooks, which increases the burden on downstream speech language models; 3) The initial channel of the codebooks contains excessive information, making it challenging to directly generate acoustic tokens from weakly supervised signals such as text in downstream tasks. Consequently, leveraging the characteristics of speech language models, we propose Language-Codec. In the Language-Codec, we introduce a Mask Channel Residual Vector Quantization (MCRVQ) mechanism along with improved Fourier transform structures and larger training datasets to address the aforementioned gaps. We compare our method with competing audio compression algorithms and observe significant outperformance across extensive evaluations. Furthermore, we also validate the efficiency of the Language-Codec on downstream speech language models.
</p>

## Model Architecture

<p align="justify">
On the far left is the encoder downsampling module, which
still utilizes the model structure of Encodec. On the far right is the decoder upsampling module, where we have
replaced it with Vocos’ model structure. the middle part is the Mask Channel Residual Vector Quantization module,
with the gray blocks indicating the masked portion of temporal information.
</p>

<table>
    <tr>
        <td ><center><img src="assets/image/arch.png"/> </center></td>
    </tr>
</table>

<p align="center">Figure.1 The overall architecture of Language-Codec.</p>


## Experiments
<p align="justify">
We evaluated the performance of the codec model on the test set of LibriTTS. The Test-Clean collection consists of 4,837 audio samples, while the Test-Other collection, which mostly contains audio recorded in noisy environments, comprises a total of 5,120 audio samples. Considering that the primary purpose of the discrete codecs is to serve as an audio representation for downstream tasks, excessive channel numbers would significantly burden downstream speech language models. Therefore, we conducted a comparison between four-channel and eight-channel dimensions. Among the objective metrics we employed, UTMOS and speaker similarity metrics closely approximate the subjective perception of human listeners. On the other hand, PESQ, STOI, and F1 metrics are more indicative of the inherent quality of the audio signal. Due to the subtle differences in UTMOS, we will highlight the top two models with the highest UTMOS scores for each channel. As for the remaining objective audio quality metrics, we will only highlight the highest-performing model. The experimental results are shown in Table 1.
</p>

<table>
    <tr>
        <td ><center><img src="assets/image/result.png"/> </center></td>
    </tr>
</table>

<p align="center">Table.1 The results of different codec models on the LibriTTS Test-Clean and Test-Other dataset.</p>

## Compare with others
<p align="justify">We provide ten sets of audio to compare the effects of languagecodec and other models.</p>
<script>
function pauseOthers(ele) {
    $("audio").not(ele).each(function (index, audio) {audio.pause();});
}
</script>

<style>
.main-content table {
    display: inline-table;
}
table {
    table-layout:fixed;
    width: 100%;
    overflow: hidden;
}
#player{
    width: 100%;
}
</style>

<p>&nbsp;</p> 
1.He felt above him the vast indifferent dome and the calm processes of the heavenly bodies; and the earth beneath him, the earth that had borne him, had taken him to her breast.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/opus_1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/evs_1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/lyra_1089_134691_000052_000000_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/encodec_1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/st_1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/1/languagecodec_1089_134691_000052_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
2.Such is their ponderous weight that they cannot rise from the horizon; but, obeying an impulse from higher currents, their dense consistency slowly yields.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/opus_260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/evs_260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/lyra_260_123288_000006_000002_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/encodec_260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/st_260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/2/languagecodec_260_123288_000006_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
3.Now let the devils strike our scent!" said the scout, tearing two rifles, with all their attendant accouterments, from beneath a bush, and flourishing "killdeer" as he handed Uncas his weapon; "two, at least, will find it to their deaths.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/opus_1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/evs_1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/lyra_1320_122617_000069_000000_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/encodec_1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/st_1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/3/languagecodec_1320_122617_000069_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
4.Well, if there is nothing to be learned here, we had best go inside.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/opus_1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/evs_1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/lyra_1580_141083_000043_000001_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/encodec_1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/st_1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/4/languagecodec_1580_141083_000043_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
5.He grasped his hoe and started briskly to work.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/opus_1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/evs_1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/lyra_1995_1826_000051_000001_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/encodec_1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/st_1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/5/languagecodec_1995_1826_000051_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
6.Critias when he told this tale of the olden time, was ninety years old, I being not more than ten.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/opus_2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/evs_2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/lyra_2961_961_000004_000002_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/encodec_2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/st_2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/6/languagecodec_2961_961_000004_000002.wav" type="audio/mpeg"></audio> </th>
    </tr>
</table>

<p>&nbsp;</p> 
7.Stung by anxiety for this little sister, she upbraided Miss W--- for her fancied indifference to Anne's state of health.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/opus_3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/evs_3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/lyra_3575_170457_000048_000000_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/encodec_3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/st_3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/7/languagecodec_3575_170457_000048_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
8.It's delightful to hear it in a London theatre.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr>
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/opus_4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/evs_4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/lyra_4446_2271_000007_000002_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/encodec_4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/st_4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/8/languagecodec_4446_2271_000007_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
9.The carey housewarming.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/opus_4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/evs_4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/lyra_4992_41806_000001_000000_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/encodec_4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/st_4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/9/languagecodec_4992_41806_000001_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

<p>&nbsp;</p> 
10.This was at the March election, eighteen fifty five.<br>
<table>
    <tr>
        <th> GT</th>
        <th> Opus(6.0kbps) </th>
        <th> EVS(7.2kbps)</th>
        <th> Lyra-v2(6.0kbps)</th>
        <th> Encodec(6.0kbps)</th>
        <th> SpeechTokenizer(6.0kbps)</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/opus_7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/evs_7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/lyra_7729_102255_000002_000003_decoded.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/encodec_7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/st_7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/audios/10/languagecodec_7729_102255_000002_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>

## More Audios 
<p align="justify">Here, we provide more audio samples to demonstrate the differences between languagecodec and GT.</p>

<p>&nbsp;</p> 
1.Let me not survive my disgrace!<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000003_000010.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000003_000010.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
2.Dr rohlfs writes to me that he found the mixed races in the great sahara, derived from arabs, berbers, and negroes of three tribes, extraordinarily fertile.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_36600_000011_000012.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_36600_000011_000012.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
3."how long ago were you arrested?" asked beth.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000057_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000057_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
4.Then i fell down at tom temple's feet.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_81414_000047_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_81414_000047_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
5."he's better now.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_81414_000049_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_81414_000049_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
6.Conclusion.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79759_000001_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79759_000001_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
7.Was the young lady naomi colebrook?<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_36377_000012_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_36377_000012_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
8.The mill was at the outskirts of the town.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000068_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000068_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
9.There was but one door to the house.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000022_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000022_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
10."all my men put their hands to their mouths and shouted.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000056_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000056_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
11."yes; she'll worry about me, i know.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000043_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000043_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
12.'and where is he staying?'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32865_000047_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32865_000047_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
13."his trial has not yet taken place, and instead of your devoting considerable of your valuable time appearing against him it would be much simpler to settle the matter right here and now."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000082_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000082_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
14.'that?<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32865_000044_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32865_000044_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
15.At the turn of the road he ran up against the tanner's boy, lars.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_85628_000008_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_85628_000008_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
16.'i take that for granted: in the nature of things it can hardly be otherwise,' i replied, a good deal startled and perplexed by the curious audacity of her interrogatory.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32866_000013_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32866_000013_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
17.We will make a little tour together, when all this shall have blown over, in a few weeks, and choose our retreat; and with the winter's snow we'll vanish from brandon, and appear with the early flowers at our cottage among the beautiful woods and hills of wales.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000048_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000048_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
18."excuse me, please.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68771_000038_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68771_000038_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
19.I've heard of your coming here, and sending, so often.'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000016_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000016_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
20."yes, sir, i plead guilty, although i've been told i ought not to confess.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000033_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000033_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
21.Then i will get me a farm and will winter in that land.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000008_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000008_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
22.That spirit belongs to the blood of our strange race; all our women were so.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000045_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000045_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
23.'you seem to be very sensible, mr de cresseron; pray tell me, frankly, what do you think of all this?'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32866_000008_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32866_000008_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
24.The church yard meteor expired, there was nothing in a moment but his ordinary smile of recognition.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32865_000006_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32865_000006_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
25.They had not undressed, or thought of taking any rest.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000009_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000009_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
26.I've come to talk with you about young gates."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000074_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000074_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
27."'and these shall follow your thralls in the same way.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000051_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000051_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
28."couldn't her parents have helped her?" inquired kenneth.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000046_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000046_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
29.That meal passed off rather pleasantly; and when we joined the ladies in the drawing room, the good vicar's enthusiastic little wife came to meet us, in one of her honest little raptures.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32865_000015_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32865_000015_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
30.As our boat flashed down the rollers into the water i made this song and sang it:<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000012_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000012_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
31.It is the only amends i ask of you for the wrong you have done me."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000003_000012.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000003_000012.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
32.He'll soon be back in town, or to brighton,' i said.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32865_000040_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32865_000040_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
33."'well, friend farmer,' laughed one, 'why such a long face?<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000036_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000036_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
34."i'll make your money loss good."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000084_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000084_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
35.The bed she too well remembered was there; and, above all, the cabinet, on which had stood the image she had taken away, was still on the same spot.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000016_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000016_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
36.He spoke simply, but paced up and down the narrow cell in front of them. it was evident that his feelings were deeper than he cared to make evident.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000054_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000054_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
37."oh! it is better to live on the sea and let other men raise your crops and cook your meals.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000016_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000016_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
38.But they'll have to do.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_76324_000019_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_76324_000019_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
39.Many mothers manage their children by means of tricks and contrivances, more or less adroit, designed to avoid direct issues with them, and to beguile them, as it were, into compliance with their wishes.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79730_000051_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79730_000051_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
40.'you have heard, of course, of mr wylder's absence?'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000027_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000027_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
41.Chapter twelve<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68771_000003_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68771_000003_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
42.'it is an antipathy-an antipathy i cannot get over, dear dorcas; you may think it a madness, but don't blame me.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000042_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000042_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
43."he was fairly prosperous before that, for mrs rogers was an energetic and sensible woman, and kept old will hard at work.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000051_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000051_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
44.Had i? had i?<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_81414_000042_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_81414_000042_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
45.There were benches for twenty men along each side.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000033_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000033_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
46.She brings down her bonnet and shawl by stealth, and before the chaise comes to the door she sends mary out into the garden with her sister, under pretense of showing her a bird's nest which is not there, trusting to her sister's skill in diverting the child's mind, and amusing her with something else in the garden, until the chaise has gone.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79730_000051_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79730_000051_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
47."'there, stand so!' i said, 'and glare and hiss at my foes.'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000005_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000005_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
48."'not yet,' i answered.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000019_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000019_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
49.These pediculi were darker coloured, and appeared different from those proper to the natives of chiloe in south america, of which he gave me specimens.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_36600_000010_000005.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_36600_000010_000005.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
50."'now start up the fire,' i said.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000029_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000029_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
51."sire, they were sent at the hour promised."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7127_75946_000014_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7127_75946_000014_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
52.It did not beckon, or indeed move at all; it was as still as the hand of death.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_81414_000014_000003.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_81414_000014_000003.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
53.The pain produced by an act of hasty and angry violence to which a father subjects his son may soon pass away, but the memory of it does not pass away with the pain.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79759_000009_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79759_000009_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
54.'rachel, dear, i have a plan for you and me: we shall be old maids, you and i, and live together like the ladies of llangollen, careless and happy recluses.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000048_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000048_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
55."nay, where it does exist."<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6930_75918_000023_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6930_75918_000023_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
56."no, indeed," he replied, frankly.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000045_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000045_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
57.Leif and grim shall be the same kind of friends to your two sons.'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_33396_000049_000004.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_33396_000049_000004.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
58.It is here manifestly impossible to select the more sterile individuals, which have already ceased to yield seeds; so that the acme of sterility, when the germen alone is affected, cannot have been gained through selection.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_36600_000012_000013.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_36600_000012_000013.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
59.Kenneth and beth went away quite happy with their success, and the manager stood in his little window and watched them depart.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000097_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000097_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
60.I am very glad.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79740_000010_000004.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79740_000010_000004.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
61."sure ly!<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000019_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000019_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
62.'can i conjecture why he is gone?' murmured rachel, still gazing with a wild kind of apathy into distance.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000034_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000034_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
63.I hope you have no prejudice against americans.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5142_36377_000010_000004.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5142_36377_000010_000004.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
64.Thank you, from my heart, for your love; you will never know, perhaps, how much it is to me.'<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000046_000002.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000046_000002.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
65."would you like that?" asked beth.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/6829_68769_000044_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_6829_68769_000044_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
66.You may wonder to hear me speak thus, being so young.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000004_000008.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000004_000008.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
67.The young queen looked on her kindly, but sadly, through her large, strange eyes, clouded with a presage of futurity, and she kissed her again, and said-<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000047_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000047_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
68.I meant to speak to him and end all between us; and i would now write, but there is no address to his letters.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5683_32879_000029_000001.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5683_32879_000029_000001.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
69.He was greatly confused at finding that he had betrayed such emotion; but his mother, who guessed his thoughts, said to him, "do not be ashamed, my son, at having been so overcome by your feelings; you would have been so still more had you known what i will no longer conceal from you, though i had intended to reserve it for a more joyful occasion.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/5639_40744_000029_000005.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_5639_40744_000029_000005.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
<p>&nbsp;</p> 
70.For the ideas and generalizations thus mainly formed from the images and impressions received in childhood become, in later years, the elements of the machinery, so to speak, by which all his mental operations are performed.<br>
<table>
    <tr>
        <th> GT</th>
        <th> LanguageCodec(6.0kbps)</th>
    </tr> 
    <tr>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/7021_79759_000008_000000.wav" type="audio/mpeg"></audio> </th>
        <th> <audio controls id="player" onplay="pauseOthers(this);"><source src="assets/more_audios/languagecodec_7021_79759_000008_000000.wav" type="audio/mpeg"></audio> </th>
    </tr> 
</table>   
            
