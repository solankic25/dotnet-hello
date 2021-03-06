# Link

-   https://docs.microsoft.com/en-us/dotnet/core/tutorials/using-on-macos

## Tutorial Steps

1. Create a dir then cd into that dir
2. run `dotnet new sln` to create `golden.sln`
3. run `dotnet new classlib -o library` produces two files,`library.csproj` and `Class1.cs`, in the library folder
4. run `dotnet sln` to add the newly created `library.csproj` project to the solution
5. run `dotnet add library package Newtonsoft.Json` to add Package Reference to Item Group in library file.
6. run `dotnet restore` similar to npm install
7. Create a `Thing` class in place of `Class1`
8. Run `dotnet build`

## Notes

-   Our library methods serialize and deserialize objects in JSON format
-   To support JSON serialization and deserialization, add a reference to the `Newtonsoft.Json` NuGet package
-   The `dotnet add` command adds new items to a project.
-   To add a reference to a NuGet package, use the `dotnet add package` command and specify the name of the package. (step 5)
-   `dotnet restore` restores dependencies and creates an obj folder inside library with three files in it, plus a `project.assets.json` file
-   Build the library with the `dotnet build` command. This produces a `library.dll` file under `golden/library/bin/Debug/netstandard1.4`:

## Testing

1. run `dotnet new xunit -o test-library` to create testing directory and unit test class
2. run `dotnet sln add test-library/test-library.csproj` to add the test project to the solution.
3. run `dotnet add test-library/test-library.csproj reference library/library.csproj`
4. Create Library Unit Test public method
5. `dotnet restore`
6. RUN THE TEST `dotnet test test-library/test-library.csproj` It should fail first `Assert.NotEqual(42, new Thing().Get(19, 23));`
7. update the test to `Assert.Equal(42, new Thing().Get(19, 23));` To pass

## Notes

-   Note that you assert the value 42 is not equal to 19+23 (or 42) when you first create the unit test (Assert.NotEqual), which will fail. An important step in building unit tests is to create the test to fail once first to confirm its logic

## Console App

1. run `dotnet new console -o app` to Create a new console application and app directory
2. run `dotnet sln add app/app.csproj` to add the console app project to the solution
3. run `dotnet add app/app.csproj reference library/library.csproj` to create the dependency on the library
4. run `dotnet restore`to restore the dependencies of the three projects in the solution
5. Open `Program.cs`

    - Replace the contents of the Main method with the following line `WriteLine($"The answer is {new Thing().Get(19, 23)}");`
    - Add two `using` directives to the top, - `using static System.Console; using Library;`

6. Run `dotnet run -p app/app.csproj` to run the executable

## Notes

-   how does it reference the dependency and what changes?
-   in `app.csproj` add
-   ```<ItemGroup>
      <ProjectReference Include="..\library\library.csproj" />
    </ItemGroup>
    ```
-   In step 6 run `dotnet run` where the `-p` option to `dotnet run` specifies the project for the main application
-   error: `Program.cs(10,13): error CS0103: The name 'Console' does not exist in the current context [/Users/gingerwilliams/source/dotnetDemo/golden/app/app.csproj]`

`The build failed. Please fix the build errors and run again.`

# Debug

1. Set a breakpoint at the `WriteLine` statement in the `Main` method.
2.
