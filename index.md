This DEMO mainly introduces ItoTTS and ItoWave, a new generation of speech synthesis technology based on Ito stochastic differential equations.


## Introduction
ItoTTS and ItoWave are designed to solve the problem of generating speech from text. We propose to use the linear Ito stochastic differential equation, under conditional input, such as original text or original sound features (such as speech mel spectrum), to use the Wiener process as a drive to gradually subtract the excess signal from the noise signal, thereby generating realistic corresponding meaningful speech. This process is a lot like Auguste Rodin carved out the thinker from the original natural stone, using carving techniques and methods to gradually remove the superfluous parts from the natural stone. Our method unifies two important aspects in speech synthesis, namely text-to-speech (TTS) and vocoder (vocoder), in one framework, which we call ItoTTS and ItoWave, respectively. This unified framework consists of two stochastic processes with solutions determined by the linear Ito stochastic differential equation and its corresponding reverse-time Ito stochastic differential equation, respectively. These two stochastic processes, especially the reverse stochastic process, can generate mel features (ItoTTS) under the condition of text input; or generate corresponding continuous sounds (ItoWave) under the condition of mel features. The experimental results show that our subjective audience MOS score reaches the highest level in the world.
<hr>

### Key modules: Score predictor

There are two key modules of our ItoTTS and ItoWave, one is a deep neural network for predicting the log speech probability density gradient value, and the other is a sampling algorithm based on the gradient value and the inverse Ito stochastic differential equation.

Deep Neural Networks for Predicting Log Speech Probability Density Gradient Values

Predictive network structure in ItoTTS


<td><img src="src/itotts_arch.jpg" width="750"></td>


Prediction network structure in ItoWave

<td><img src="src/itowave_arch.jpg" width="750"></td>
  
### Audio samples

#### Short samples
You can listen to some sound samples synthesized by ItoTTS and ItoWave. The corresponding text is as follows:

1. but they proceeded in all seriousness, and would have shrunk from no outrage or atrocity in furtherance of their foolhardy enterprise.
               
2. three cars for press photographers, an official party bus for white house staff members and others, and two press buses.
               
3. a base station at a fixed location in dallas operated a radio network which linked together the lead car,
               
4. the lifting had been so complete in this case that there was no trace of the print on the rifle itself when it was examined by latona.
               
5. with the active cooperation of the responsible agencies and with the understanding of the people of the united states in their demands upon their president,

##### Comparison of synthetic effects between ItoTTS and other TTS systems

<table style='text-align: center;'>
  <tbody>
    <tr>
      <td>Ground truth</td>
      <td>FastSpeech 2</td>
      <td>Tacotron 2</td>
     <td>ItoTTS</td>
    </tr>
    <tr>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/fastspeech2/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/tacotron2/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itotts/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
          <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ030-0100.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/fastspeech2/LJ030-0100.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/tacotron2/LJ030-0100.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itotts/LJ030-0100.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ030-0106.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/fastspeech2/LJ030-0106.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/tacotron2/LJ030-0106.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itotts/LJ030-0106.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ032-0137.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/fastspeech2/LJ032-0137.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/tacotron2/LJ032-0137.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itotts/LJ032-0137.wav" type="audio/wav" /></audio></td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
        <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ050-0277.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/fastspeech2/LJ050-0277.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/tacotron2/LJ050-0277.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itotts/LJ050-0277.wav" type="audio/wav" /></audio></td>
    </tr>
  </tfoot>
</table>

<hr>

##### Synthesis effect comparison between ItoWave and other vocoder systems
<table style='text-align: center;'>
  <tbody>
    <tr>
      <td>Ground truth</td>
      <td>WaveNet</td>
      <td>WaveGlow</td>
     <td>DiffWave</td>
      <td>WaveGrad</td>
      <td>ItoWave</td>
    </tr>
    <tr>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavenet/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/waveglow/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/diffwave/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavegrad/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itowave/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
    <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavenet/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/waveglow/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/diffwave/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavegrad/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itowave/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
   <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavenet/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/waveglow/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/diffwave/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavegrad/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itowave/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
   <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavenet/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/waveglow/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/diffwave/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavegrad/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itowave/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
   <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/groundtruth/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavenet/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/waveglow/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/diffwave/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/wavegrad/LJ010-0062.wav" type="audio/wav" /></audio></td>
      <td><audio controls="" style="width: 160px;height: 50px"><source src="src/waves_for_github/itowave/LJ010-0062.wav" type="audio/wav" /></audio></td>
    </tr>
  </tfoot>
</table>

#### Long samples 


<table style='text-align: center;'>
  <tbody>
    <tr>
      <td></td>
      <td>KaraSinger</td>
    </tr>
    <tr>
      <td>Sample 1</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics1/temp0.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 2</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics1/temp1.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 3</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics1/temp2.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 4</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics1/temp3.wav" type="audio/wav" /></audio></td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Sample 5</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics1/temp4.wav" type="audio/wav" /></audio></td>
    </tr>
  </tfoot>
</table>



<table style='text-align: center;'>
  <tbody>
    <tr>
      <td></td>
      <td>KaraSinger</td>
    </tr>
    <tr>
      <td>Sample 1</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics2/temp0.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 2</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics2/temp1.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 3</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics2/temp2.wav" type="audio/wav" /></audio></td>
    </tr>
    <tr>
      <td>Sample 4</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics2/temp3.wav" type="audio/wav" /></audio></td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Sample 5</td>
      <td><audio controls=""><source src="./assets/audios/long/lyrics2/temp4.wav" type="audio/wav" /></audio></td>
    </tr>
  </tfoot>
</table>

<hr>

### Contact 
wu.shoule@protonmail.com, shiziqiang7@gmail.com, 13621160486

