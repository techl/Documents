# Merge Assemblies 

Add Nuget package 'ILRepack.MSBuild.Task'

For MSBuild project
```
  <Target Name="AfterBuild" Condition="'$(Configuration)' == 'Release'">

    <!-- List of assemblies to merge, you must start with the main dll/exe, so you can use SameAsPrimaryAssembly later -->
    <ItemGroup>
      <InputAssemblies Include="$(TargetPath)" /> <!-- Output file of the project -->
      <InputAssemblies Include="$(OutputPath)\Newtonsoft.Json.dll" />
    </ItemGroup>

    <!-- ILRepack task -->
    <ILRepack
        Parallel="true"
        Internalize="true"
        InternalizeExclude="@(DoNotInternalizeAssemblies)"
        InputAssemblies="@(InputAssemblies)"
        TargetKind="SameAsPrimaryAssembly"
        OutputFile="$(TargetPath)" />

  </Target>
```

For .Net Core Project
```
  <Target Name="ILRepack" AfterTargets="Build">
    <!-- List of assemblies to merge -->
    <ItemGroup>
      <InputAssemblies Include="$(TargetPath)" /> <!-- Output file of the project -->
      <InputAssemblies Include="@(ReferencePathWithRefAssemblies)" Condition="'%(filename)' == 'Newtonsoft.Json'" />
    </ItemGroup>

    <!-- ILRepack task -->
    <ILRepack
        Parallel="true"
        Internalize="true"
        InternalizeExclude="@(DoNotInternalizeAssemblies)"
        InputAssemblies="@(InputAssemblies)"
        TargetKind="SameAsPrimaryAssembly"
        OutputFile="$(TargetPath)" />

  </Target>
```

*Currently, it works only in Release Mode.*

Reference :  
https://www.meziantou.net/2018/08/28/merging-assemblies-using-ilrepack

