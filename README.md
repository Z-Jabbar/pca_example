# pca_example
A MATLAB snippet demonstrating PCA feature extraction
% PCA Feature Extraction Snippet
%
% This MATLAB code snippet demonstrates:
% - PCA feature extraction from a test image
% - Calculation of Euclidean distances to projected training images
%
% NOTE:
% - This is only a part of the full PCA project (Eigenfaces)
% - To run this code fully, you need:
%   - Precomputed Eigenfaces
%   - Centered training images (ProjectedImages)
%   - The variable 'm' (mean image)
%   - The variable 'Train_Number'

%%%%%% Extracting the PCA features from test image
image = imread(TestImage);
image = im2gray(image);
image = imresize(image, [64 80]);
im1h=histeq(image);
imd=double(im1h);
im1hn = imd-mean(imd(:));
InputImage = im1hn/std(im1hn(:));

%InImage = reshape(temp',irow*icol,1);
InImage=reshape(InputImage',64*80, 1);
Difference = double(InImage)-m; % Centered test image
ProjectedTestImage = Eigenfaces'*Difference; % Test image feature vector

%%%%% Calculating Euclidean distances 
%d = sum(abs(bsxfun(@minus,p,w)),2);
Euc_dist = [];
for i = 1 : Train_Number
    q = ProjectedImages(:,i);
 
    temp = sum(abs(bsxfun(@minus,ProjectedTestImage,q))) ;
    Euc_dist = [Euc_dist temp];
end
[Euc_dist_min , Recognized_index] = min(Euc_dist);
OutputName = strcat(int2str(Recognized_index),'.pgm');
end
