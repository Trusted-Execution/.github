# Trusted Execution 

This is the home of the Trusted Execution lab here at the University of Hawaii's College of Engineering
<img src="https://github.com/Trusted-Execution/.github/blob/main/profile/CollegeofEngineeringLogo.png"
     alt="CoE Logo" align="right" width="100" />
Our research is focused on techniques to improve the security of our data and applications in an era of increasing cyber threats.

## Terminology

Language is important... ABIs, APIs and English are all variations of the same theme:  An agreement amongst authors on a set of conventions for communicating information.  To that end, there's some terminilogy that we should identify up-front and try to use it consistently throughout this project:

- **Executable**:  A file that contains executable code.  Generally executables can be either a Library or a Main
- **Library**:  An executable that's intended to be shared by several Main files
- **Main**:  An executable with an entry point
- **Static Main**:  An executable that's been statically compiled and needs no Libraries
- **User Process**:  This is an instance of exactly 1 copy of ld, 1 Main and zero or more Libraries.
  -- Within a normal process, executables have no mechanism to keep secrets from each other
  -- Within a normal process, there is no mechanism to that an executable can use to make risk decisions about which Library to bind to it (libraries can have dependencies on other libraries)
  -- Within a normal process, there is no mechanism to ensure that an executable is genuine


## SGX Features this project will use
This stuff you'll have to pay attention to

## SGX Features this projecg will not use
You'll see references to these things in the documentation, but you can safely ignore this stuff for this project.

