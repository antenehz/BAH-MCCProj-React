node {
    
    stage ("Checkout React Client"){
        git branch: 'main', url: 'https://github.com/abarbuzza/BAH-MCCProj-React.git'
    }
    
    stage ("Install dependencies - React Client") {
        'npm install'
    }
    
    stage ("Launch - React Client") {
        'npm start'
    }
}
    
