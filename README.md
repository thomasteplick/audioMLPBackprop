<h3>Audio Recognition/Classification using a MLP Neural Network with the Back-Propagation Algorithm</h3>
<hr>
This program is a web application written in Go that makes extensive use of the html/template package.
Navigate to the C:\Users\your-name\AudioMLPBackprop\src\backprop\ directory and issue "go run audiomlp.go" to
start the Multilayer Perceptron Neural Network server. In a web browser enter http://127.0.0.1:8080/audioMLP
in the address bar.  There are two phases of operation:  the training phase and the testing phase.  During the training
phase, examples consisting of wav audio and the desired class are supplied to the network.  The wav audio files are submitted
to Fourier Analysis using the Fast Fourier Transform (FFT) and the Spectral Power Density in magnitude squared is created.
The mean of the PSD is removed and the magnitude is normalized to one to prevent the gradient from saturating and slowing the learning process.
The network itself is a directed graph consisting of an input layer of the images, one or more hidden layers of a given depth, and
an output layer of nodes.  The nodes of the network are connected by weighted links.
The network is fully connected.  This means that every node is connected to its immediately adjacent neighbor node.  The weights are trained
by first propagating the inputs forward, layer by layer, to the output layer of nodes.  The output layer of nodes finds the
difference between the desired and its output and back propagates the errors to the input layer.  The hidden and input layer
weights are assigned “credit” for the errors by using the chain rule of differential calculus.  Each neuron consists of a
linear combiner and an activation function.  This program uses the hyperbolic tangent function to serve as the activation function.
This function is non-linear and differentiable and limits its output to be between -1 and 1.  <b>The purpose of this program is to classify an
audio waveform stored in a wav audio file</b>.
The user selects the MLP training parameters:
<li>Epochs</li>
<li>Learning Rate</li>
<li>Hidden Layers</li>
<li>Layer Depth</li>
<li>FFT Size</li>
<li>FFT Window</li>
<br />
<p>
The <i>Learning Rate</i> is between .01 and .00001.  Each <i>Epoch</i> consists of 16 <i>Training Examples</i>.  
One training example is a Power Spectral Density (mag^2) and the desired class (0, 1,…, 15).  There are 16 audio wav files and therefore 16 classes.
The WAV audio files were produced using the Generate Audio page.  The user selects the SNR in
dB (-10,-50).  The program generates 16 wav audio files consisting of 8,192 16-bit samples of 8-12 sinusoids using a sampling frequency of 4,000 Hz (64kbps).  This
produces a two-second wav audio file.  The 16 sinsuoids are between 60 and 1920 Hz, at multiples of 60.  Since the sampling rate is 4,000 Hz, the Nyquist frequency 
is 2,000 Hz and frequencies above this are aliased.  Gaussian noise is added to the sinsuoidal sum with zero mean and standard deviation depending on the SNR.
</p>
<p>
When the <i>Submit</i> button on the MLP Training Parameters form is clicked, the weights in the network are trained
and the Learning Curve (mean-square error (MSE) vs epoch) is graphed.  As can be seen in the screen shots below, there is significant variance over the ensemble,
but it eventually settles down after about 100 epochs. An epoch is the forward and backward propagation of all the 16 training samples.
</p>
<p>
When the <i>Test</i> link is clicked, 16 examples are supplied to the MLP  It classifies the audio wav files.
The test results are tabulated and the actual PSD images are graphed from the wav files that were supplied to the MLP
It takes some trial-and-error with the MLP Training Parameters to reduce the MSE to zero.  It is possible to a specify a 
more complex MLP than necessary and not get good results.  For example, using more hidden layers, a greater layer depth,
or over training with more examples than necessary may be detrimental to the MLP.  Clicking the <i>Train</i> link starts a new training
phase and the MLP Training Parameters must be entered again.
</p>
<p>
 In the <i>Generate Audio</i> and <i>Train</i> pages, the user can select the form of the PSD generated.  Either Bartlett or Welch
 variant can be chosen.  The window type can be selected from among Bartlett, Hamming, Hanning, and  Welch.  These are used
 with 50% overlap between FFT sections.  The Rectangle window does not use overlap.  The number of FFT sections depends on
 the FFT size chosen.  Smaller FFTs have more sections which are summed and averaged.  This reduces the variance of the PSD.
</p>

<b>Generate Audio Wav Files, 0dB SNR, FFT Size 1024, FFT Window Hamming
![image](https://github.com/user-attachments/assets/9f9a4230-28f5-4955-9b32-0de5172cb365)

<b>Audio Recognition Learning Curve, MSE vs Epoch, One Hidden Layer, 20 nodes/neurons deep, FFT Size 8192, FFT Window Rectangle,</b>
<b>0dB SNR, Learning Rate .01, Epochs 100</b>
![image](https://github.com/user-attachments/assets/a56c1ca4-2374-46c2-855f-a282d50185a6)

<b>Audio Recognition Test Results, One Hidden Layer, 20 nodes/neurons deep, FFT Size 8192, FFT Window Rectangle,</b>
<b>0dB SNR, Learning Rate .01, Epochs 100</b>
![image](https://github.com/user-attachments/assets/5014f9a9-0768-4d3a-9c9e-afa0ee74322a)
